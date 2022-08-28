# Instalasi dan Konfigurasi Gitlab CI dan Docker Kontainer Ubuntu 20.04 LTS

# 1. Instalasi Gitlab CI
GitLab adalah repositori kode berbasis web gratis dan open-source untuk pengembangan perangkat lunak kolaboratif. Gitlab adalah salah satu dari banyak tool DevOps yang digunakan oleh DevOps Engineer.
Pada kesempatan kali ini saya ingin mencoba memberikan tutorial instalasi dan konfigurasi Gitlab CI pada server Ubuntu 20.04 LTS, Selamat mencoba

## Prasyarat
### 1.  Perbaharui Sistem Operasi
```sh
sudo apt update && sudo apt upgrade -y
```
### 2.  Instal Dependensi Gitlab
```sh
sudo apt install curl ca-certificates apt-transport-https gnupg2 -y
```
### 3. Buat & Impor Repositori GitLab
Secara default, GitLab tidak dikemas dalam repositori default Ubuntu, dan ini berarti kita harus membuatnya secara manual. GitLab telah membuat skrip APT yang berguna untuk kita unduh dan jalankan agar membantu kita dalam proses instalasi ini.
```sh
curl -s https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | sudo bash
```
### 4. Jalankan perintah apt update untuk memverifikasi dan menyinkronkan repositori baru
```sh
sudo apt update
```
### 5. Instalasi Gitlab
```sh
sudo apt install gitlab-ce
```
### 6. Konfigurasi Gitlab
Dengan menginstal GitLab, kita sekarang dapat mengonfigurasi SSL, kata sandi nama domain atau nama subdomain, dan banyak lagi. Tutorial akan membahas opsi pengaturan dasar yang harus dilakukan. Namun, kita dapat melakukan pengaturan alternatif untuk yang tercantum di dalam file gitlab.rb
Gunakan teks editor kesayangan kalian seperti vi, vim, dan nano untuk mengedit file tersebut.
```sh
sudo nano nano /etc/gitlab/gitlab.rb
```
- Pengaturan pertama adalah mengatur domain, menavigasi ke baris 36, uncomment lalu isi sesuai domain yang kamu inginkan.
  
```sh
external_url 'https://gitlab."isi_domain_kamu".com'
```
- Secara default, semua pengaturan dikomentari dengan "#." kamu harus menghapus komentar pada baris berikut.

```sh
 letsencrypt['enable'] = true
 letsencrypt['contact_emails'] = ['youremail@domain_kamu.com']
 letsencrypt['auto_renew'] = true
 letsencrypt['auto_renew_hour'] = 4
 letsencrypt['auto_renew_day_of_month'] = "*/4"
 letsencrypt['auto_renew_log_directory'] = '/var/log/gitlab/lets-encrypt'
```
- Setelah selesai, simpan konfigurasi dan jalan perintah berikut untuk reconfigure 

```sh
sudo gitlab-ctl reconfigure
```

### 7. Verifikasi instalasi Gitlab dengan mengakses domain kamu melalui browser
```sh
https://gitlab."isi_domain_kamu".com
```
Jika Gitlab sudah dapat diakses melalui browser silahkan lanjutkan dengan register akun baru, panduan pada link berikut 

```sh
https://www.youtube.com/watch?v=YqJdgNbfAyc
```

Selamat Kamu sudah berhasil melakukan instalasi Gitlab


# 2. Instalasi Docker pada Ubuntu 20.04 LTS
Docker adalah aplikasi untuk menyatukan berbagai file software dan pendukungnya dalam sebuah kontainer agar memudahkan proses pengembangan software.

mengapa kita perlu menggunakan container seperti yang ditawarkan Docker?

Dalam pengembangan aplikasi, developer memerlukan virtualisasi di server agar aplikasi bisa berjalan di berbagai platform dengan konfigurasi hardware yang berbeda-beda.

Sayangnya, ketika menggunakan virtualisasi, kita harus menyiapkan satu sistem operasi secara penuh. Jika membutuhkan beberapa virtualisasi, server perlu resource yang besar.
Kontainer bisa digunakan sebagai alternatif virtualisasi sehingga tidak perlu menyiapkan sistem operasi secara penuh. Dengan kontainer, ukuran file menjadi lebih kecil dibandingkan virtualisasi yang biasa digunakan.

### 1. Update Sistem
```sh
 sudo apt update
```

### 2. Install Package yang Dibutuhkan
Ada beberapa package yang dibutuhkan dalam instalasi Docker. Jalankan perintah di bawah ini untuk download package-package tersebut.
```sh
 sudo apt-get install curl apt-transport-https ca-certificates software-properties-common
```

### 3. Tambahkan Repositori Docker
- Tambahkan GPG key
```sh
 curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
- Tambahkan repositori Docker
```sh
 sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
- Pastikan Anda menginstal dari repositori Docker, bukan repositori Ubuntu
```sh
 apt-cache policy docker-ce
```
### 4. Install Docker
```sh
 sudo apt install docker-ce
```
### 5. Cek Instalasi Docker
```sh
 sudo systemctl status docker
```

Pastikan hasilnya adalah loaded dengan status Active (running). Selamat kamu sudah berhasil mengintsal Docker











**Credit by Falyan Zuril**

[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [dill]: <https://github.com/joemccann/dillinger>
   [git-repo-url]: <https://github.com/joemccann/dillinger.git>
   [john gruber]: <http://daringfireball.net>
   [df1]: <http://daringfireball.net/projects/markdown/>
   [markdown-it]: <https://github.com/markdown-it/markdown-it>
   [Ace Editor]: <http://ace.ajax.org>
   [node.js]: <http://nodejs.org>
   [Twitter Bootstrap]: <http://twitter.github.com/bootstrap/>
   [jQuery]: <http://jquery.com>
   [@tjholowaychuk]: <http://twitter.com/tjholowaychuk>
   [express]: <http://expressjs.com>
   [AngularJS]: <http://angularjs.org>
   [Gulp]: <http://gulpjs.com>

   [PlDb]: <https://github.com/joemccann/dillinger/tree/master/plugins/dropbox/README.md>
   [PlGh]: <https://github.com/joemccann/dillinger/tree/master/plugins/github/README.md>
   [PlGd]: <https://github.com/joemccann/dillinger/tree/master/plugins/googledrive/README.md>
   [PlOd]: <https://github.com/joemccann/dillinger/tree/master/plugins/onedrive/README.md>
   [PlMe]: <https://github.com/joemccann/dillinger/tree/master/plugins/medium/README.md>
   [PlGa]: <https://github.com/RahulHP/dillinger/blob/master/plugins/googleanalytics/README.md>
