# Responsi-TeknologiCloud-Riska
 
# 1. Persiapan

****1.1. Buat Direktori********

Buat dua direktori yaitu website-utama dan website-profil.

_mkdir website-utama website-profil_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/c422807f-579d-4865-9107-9ee57cfcb597)

**1.2. Buat file HTML di dalam direktori website-utama**

Buat file index.html di dalam direktori website-utama.

_nano website-utama/index.html_

Isi file index.html dengan konten berikut

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/d6a85906-f6fb-469b-a9f1-0e82016dcca5)

Pembahasan :


**1.3. Buat file HTML di dalam direktori website-profil**

Buat file index.html di dalam direktori website-profil.

_nano website-profil/index.html_

Isi file index.html dengan konten berikut:

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/4f09ff2b-b840-4672-8ba9-5d42f8f6eb99)

Pembahasan :


# 2. Buat Docker Network

Buat jaringan Docker dengan nama my-Riska-Novita-Situmorang-network

_docker network create my-Riska-Novita-Situmorang-network_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/b0b4080f-af50-4a7f-958a-2a0a92cd0340)

Pembahasan :


# 3. Buat Dockerfile dan Image

**3.1. Dockerfile untuk Website Utama**
Buat file Dockerfile di dalam direktori website-utama.

_nano website-utama/Dockerfile_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/11b91303-c8b6-4c3c-a829-161cda32a70e)

Isi file Dockerfile dengan konten berikut:

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/feab2a8e-ac0a-4875-b173-9feb5effd004)

**3.2. Dockerfile untuk Website Profil**
Buat file Dockerfile di dalam direktori website-profil.

_nano website-profil/Dockerfile_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/f9df69c8-d485-4353-9d61-2cb526f52a59)

Isi file Dockerfile dengan konten berikut:

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/4305e9e3-7712-4336-8dfb-e19153be6d91)

# 4. Build Image
Bangun dua image Docker dari Dockerfile yang sudah dibuat.

_cd website-utama_

_docker build -t website-utama ._

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/991d8d6c-486b-44bf-a12d-0daa46e1ca64)

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

# 6. Menjalankan Container
Jalankan container dengan menyambungkan ke Docker network yang sudah dibuat.

6.1. Jalankan Container Website Utama
Jalankan container website-utama.

_docker run -d --name website-utama --network my-Riska-Novita-Situmorang-network -p 8080:80 website-utama_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/c6ca4ce4-abd9-4ce0-8098-b7a47f1f7d6d)

6.2. Jalankan Container Website Profil
Jika menggunakan volume:

_docker run -d --name website-profil --network my-nama-mahasiswa-network -v profile-images:/usr/share/nginx/html/profile -p 8081:80 website-profil_

Jika tidak menggunakan volume:

_docker run -d --name website-profil --network my-Riska-Novita-Situmorang-network -p 8081:80 website-profil_

![image](https://github.com/riskasitumorang/Responsi-TeknologiCloud-Riska/assets/136875985/d21a68a8-f2bd-481e-8105-1772efb8090d)



# Pengujian
Akses website utama melalui browser: http://<IP_Address>:8080.

Klik link "profil" dan pastikan link tersebut mengarah dan menampilkan gambar profil Anda di http://<IP_Address>:8081/foto.jpg.

 
