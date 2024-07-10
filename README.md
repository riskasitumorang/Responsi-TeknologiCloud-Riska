# Responsi-TeknologiCloud-Riska
 
# 1. Persiapan

**1.1. Buat Direktori**

Buat dua direktori yaitu website-utama dan website-profil.

_mkdir website-utama website-profil_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/a3642b2f-c994-49ba-b40f-c05a8208ac2b)

Pembahasan :

Perintah mkdir website-utama website-profil digunakan untuk membuat dua direktori baru bernama website-utama dan website-profil. Direktori ini akan digunakan untuk menyimpan file HTML dan Dockerfile yang terkait dengan masing-masing website. Dengan membuat direktori terpisah, struktur proyek menjadi lebih terorganisir dan mudah dikelola.


**1.2. Buat file HTML di dalam direktori website-utama**

_nano website-utama/index.html_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/e794c1f0-c9fa-49af-9b8c-b97bce87ade9)

Pembahasan : 

Perintah nano website-utama/index.html membuka editor teks Nano untuk membuat dan mengedit file HTML bernama index.html di dalam direktori website-utama. File ini akan berfungsi sebagai halaman utama dari website utama.


Isi file index.html dengan kode berikut

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/d6a85906-f6fb-469b-a9f1-0e82016dcca5)

Pembahasan :

Kode HTML ini adalah struktur dasar dari sebuah halaman web. Tag <title> menetapkan judul halaman yang akan ditampilkan pada tab browser. Tag h1 digunakan untuk judul utama di halaman, dan tag p berisi tautan ke halaman profil dengan menggunakan tag <a>. Tautan ini akan mengarahkan pengguna ke website profil yang berjalan di port 8081.


**1.3. Buat file HTML di dalam direktori website-profil**

_nano website-profil/index.html_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/df2d7244-1330-4437-80be-94a2ade5c4a9)

Pembahasan :

Perintah nano website-profil/index.html membuka editor teks Nano untuk membuat dan mengedit file HTML bernama index.html di dalam direktori website-profil. File ini akan berfungsi sebagai halaman utama dari website profil.

Isi file index.html dengan konten berikut:

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/4f09ff2b-b840-4672-8ba9-5d42f8f6eb99)

Pembahasan :

Kode HTML ini menampilkan halaman profil dengan judul "Profil Anda". Tag <img> digunakan untuk menampilkan gambar profil yang diambil dari file foto.jpg. Gambar ini akan disalin ke dalam kontainer Docker dan ditampilkan saat halaman profil diakses.

# 2. Buat Docker Network

Buat jaringan Docker dengan nama my-Riska-Novita-Situmorang-network

_docker network create my-Riska-Novita-Situmorang-network_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/b0b4080f-af50-4a7f-958a-2a0a92cd0340)

Pembahasan :

Perintah docker network create my-Riska-Novita-Situmorang-network digunakan untuk membuat jaringan Docker dengan nama my-Riska-Novita-Situmorang-network. Jaringan ini memungkinkan kontainer yang berjalan di dalamnya untuk saling berkomunikasi menggunakan nama layanan (service name) sebagai DNS.


# 3. Buat Dockerfile dan Image

**3.1. Dockerfile untuk Website Utama**

_nano website-utama/Dockerfile_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/11b91303-c8b6-4c3c-a829-161cda32a70e)

Pembahasan :

Perintah nano website-utama/Dockerfile membuka editor teks Nano untuk membuat dan mengedit Dockerfile di dalam direktori website-utama. Dockerfile ini akan berisi instruksi untuk membangun image Docker untuk website utama.


Isi file Dockerfile dengan kode berikut:

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/feab2a8e-ac0a-4875-b173-9feb5effd004)

Pembahasan :

Dockerfile ini menggunakan image dasar nginx:alpine, yang merupakan versi ringan dari Nginx. Instruksi COPY index.html /usr/share/nginx/html/index.html menyalin file index.html dari direktori kerja saat ini ke direktori default Nginx di dalam kontainer. Ini memungkinkan Nginx untuk menyajikan halaman web yang telah kita buat.

**3.2. Dockerfile untuk Website Profil**

_nano website-profil/Dockerfile_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/f9df69c8-d485-4353-9d61-2cb526f52a59)

Pembahasan :

Perintah nano website-profil/Dockerfile membuka editor teks Nano untuk membuat dan mengedit Dockerfile di dalam direktori website-profil. Dockerfile ini akan berisi instruksi untuk membangun image Docker untuk website profil.

Isi file Dockerfile dengan konten berikut:

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/4305e9e3-7712-4336-8dfb-e19153be6d91)

Pembahasan :

Dockerfile ini juga menggunakan image dasar nginx:alpine. Selain menyalin file index.html, instruksi COPY foto.jpg /usr/share/nginx/html/foto.jpg menyalin file gambar foto.jpg ke direktori default Nginx. Ini memungkinkan halaman profil untuk menampilkan gambar yang diinginkan.	

# 4. Build Image
Bangun dua image Docker dari Dockerfile yang sudah dibuat.

_cd website-utama_

_docker build -t website-utama ._

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/991d8d6c-486b-44bf-a12d-0daa46e1ca64)

Pembahasan :

Perintah cd website-utama dan cd ../website-profil digunakan untuk berpindah ke direktori yang sesuai. Perintah docker build -t website-utama . dan docker build -t website-profil . digunakan untuk membangun image Docker dari Dockerfile yang ada di direktori masing-masing. Opsi -t memberi nama pada image yang dibangun, sehingga lebih mudah untuk dikelola dan diidentifikasi.

_cd ../website-profil_

_docker build -t website-profil ._

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/8e08336a-2793-43d4-966a-f50533c5a291)


# 5. Docker Volume (Opsional)

Buat volume bernama profile-images.

_docker volume create profile-images_

_docker run -d --name temp-container -v profile-images:/data busybox_

_docker cp website-profil/foto.jpg temp-container:/data/_

_docker rm -f temp-container_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/52e02325-6d9b-4556-9421-2a5129ad5a86)

Pembahasan :

Perintah docker volume create profile-images membuat volume Docker bernama profile-images. Volume ini digunakan untuk menyimpan data persisten yang dapat diakses oleh kontainer. Perintah docker run -d --name temp-container -v profile-images:/data busybox menjalankan kontainer sementara dengan volume yang terpasang. Perintah docker cp website-profil/foto.jpg temp-container:/data/ menyalin file gambar ke dalam volume, dan docker rm -f temp-container menghapus kontainer sementara setelah file berhasil disalin.

# 6. Menjalankan Container
Jalankan container dengan menyambungkan ke Docker network yang sudah dibuat.

6.1. Jalankan Container Website Utama
Jalankan container website-utama.

_docker run -d --name website-utama --network my-Riska-Novita-Situmorang-network -p 8080:80 website-utama_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/c6ca4ce4-abd9-4ce0-8098-b7a47f1f7d6d)

Pembahasan :

Perintah docker run -d --name website-utama --network my-Riska-Novita-Situmorang-network -p 8080:80 website-utama menjalankan kontainer dari image website-utama dengan nama website-utama. Opsi --network my-Riska-Novita-Situmorang-network menyambungkan kontainer ke jaringan Docker yang telah dibuat. Opsi -p 8080:80 memetakan port 80 di dalam kontainer ke port 8080 di host, sehingga website utama dapat diakses melalui port 8080.

6.2. Jalankan Container Website Profil

_docker run -d --name website-profil --network my-Riska-Novita-Situmorang-network -p 8081:80 website-profil_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/d21a68a8-f2bd-481e-8105-1772efb8090d)

Pembahasan :

Perintah docker run -d --name website-profil --network my-Riska-Novita-Situmorang-network -p 8081:80 website-profil menjalankan kontainer dari image website-profil dengan nama website-profil. Opsi --network my-Riska-Novita-Situmorang-network menyambungkan kontainer ke jaringan Docker yang telah dibuat. Opsi -p 8081:80 memetakan port 80 di dalam kontainer ke port 8081 di host, sehingga website profil dapat diakses melalui port 8081.

# Pengujian

Klik Traffic / Ports

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/eb9f3e1d-4732-4a4f-97f2-2e0adddb0cf3)

Akses website utama melalui browser: http://<IP_Address>:8080.

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/799b6c2d-4a3a-4ee5-a7a0-cdb0e84dba3e)


![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/db5f6862-64f2-4705-8958-be5d1b31c107)


Klik link "profil" dan pastikan link tersebut mengarah dan menampilkan gambar profil Anda di http://<IP_Address>:8081/foto.jpg.

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/0c426be3-0b9b-40c5-bd88-5cf65bf324b2)


