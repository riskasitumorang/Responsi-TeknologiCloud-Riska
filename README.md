# Responsi-TeknologiCloud-Riska
 
1. Persiapan
1.1. Buat Direktori
Buat dua direktori yaitu website-utama dan website-profil.

bash
Salin kode
mkdir website-utama website-profil
1.2. Buat file HTML di dalam direktori website-utama
Buat file index.html di dalam direktori website-utama.

bash
Salin kode
nano website-utama/index.html
Isi file index.html dengan konten berikut:

html
Salin kode
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Halaman Utama</title>
</head>
<body>
    <h1>Halaman Utama</h1>
    <p>Nama Lengkap: Riska Novita Situmorang</p>
    <p>NIM: 215610066</p>
    <p>Program Studi: Sistem Informasi</p>
    <p>Hobi: Nyanyi</p>
    <a href="/profil">Profil</a>
</body>
</html>
1.3. Letakkan file gambar profil di dalam direktori website-profil
Salin foto profil Anda (misalnya foto.jpg) ke dalam direktori website-profil.

2. Buat Docker Network
Buat jaringan Docker dengan nama my-nama-mahasiswa-network.

bash
Salin kode
docker network create my-nama-mahasiswa-network
3. Buat Dockerfile dan Image
3.1. Dockerfile untuk Website Utama
Buat file Dockerfile di dalam direktori website-utama.

bash
Salin kode
nano website-utama/Dockerfile
Isi file Dockerfile dengan konten berikut:

Dockerfile
Salin kode
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
3.2. Dockerfile untuk Website Profil
Buat file Dockerfile di dalam direktori website-profil.

bash
Salin kode
nano website-profil/Dockerfile
Isi file Dockerfile dengan konten berikut:

Dockerfile
Salin kode
FROM nginx:latest
COPY . /usr/share/nginx/html
EXPOSE 80
4. Build Image
Bangun dua image Docker dari Dockerfile yang sudah dibuat.

bash
Salin kode
cd website-utama
docker build -t website-utama .

cd ../website-profil
docker build -t website-profil .
5. Docker Volume (Opsional)
Buat volume bernama profile-images.

bash
Salin kode
docker volume create profile-images
Salin gambar profil ke dalam volume ini.

bash
Salin kode
docker run -d --name temp-container -v profile-images:/data busybox
docker cp website-profil/foto.jpg temp-container:/data/
docker rm -f temp-container
6. Menjalankan Container
Jalankan container dengan menyambungkan ke Docker network yang sudah dibuat.

6.1. Jalankan Container Website Utama
Jalankan container website-utama.

bash
Salin kode
docker run -d --name website-utama --network my-nama-mahasiswa-network -p 8080:80 website-utama
6.2. Jalankan Container Website Profil
Jika menggunakan volume:

bash
Salin kode
docker run -d --name website-profil --network my-nama-mahasiswa-network -v profile-images:/usr/share/nginx/html/profile -p 8081:80 website-profil
Jika tidak menggunakan volume:

bash
Salin kode
docker run -d --name website-profil --network my-nama-mahasiswa-network -p 8081:80 website-profil
Pengujian
Akses website utama melalui browser: http://<IP_Address>:8080.
Klik link "profil" dan pastikan link tersebut mengarah dan menampilkan gambar profil Anda di http://<IP_Address>:8081/foto.jpg.

 
