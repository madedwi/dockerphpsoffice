# Maxomorra Docker

[![N|Solid](https://www.docker.com/sites/default/files/vertical.png)](https://www.docker.com)

Jaman sekarang tidak perlu susah susah install xampp 5 / 7 dan mysql secara manual lagi. Ngoding sudah ribet jangan dibikin ribet lagi, ngoding aja.

  - Menjalankan php 5 dan 7 secara bersamaan.
  - Optional service mysql (sebenarnya lebih simple pake ini, tidak perlu konfigurasi server mysql lagi).
  - Bebas stress.

## Langkah install !

  - Clone repo ini, dan buka file `docker-compose.yml`
  - Edit pada bagian `Volume` untuk services `maxomorra` dan `meyaboo` menjadi path www/sites/htdocs entah apa namanya tempat anda meletakkan file-file maxomorra/meyaboo seperti `<path-lokal-anda>:/var/www/html`, contoh misalnya path lokal saya adalah `/opt/def/sites` maka
  
      ```
        volumes:
        - /opt/def/sites:/var/www/html
    ```

### Konfigurasi IP address.

  Biarkan saja IP yang default di konfigurasi kalau gak mau ribet, kalau mau ribet cari tau sendiri ya.
  Ini adalah daftar ip-ip yang penting:
  
  - Untuk IP yang dilihat oleh docker, alias settingan IP server mysql yang akan kita set di konfigurasi website, pada linux ketikkan perintah `ip addrr` lihat bagian interface `docker0`. biasanya sih `172.17.0.1`.
  - Untuk IP yang dilihat oleh host, alias komputer kita sendiri, ssh ke container docker dengan cara,
    `docker exec -it <container-id> bash -l`. Dapatkan container-id dengan perintah `docker ps`. Setelah ssh ke continer, lakukan seperti langkah diatas. (perintah di windows menyusul)
  - (Optional), Tambahkan entry di file `hosts` supaya service `meyaboo` dan `maxomorra` memiliki nama domain sendiri
      ```
      ...
      73.0.0.10   php7
      73.0.0.20   php56 
      ...
      ``` 
    - Di linux file `etc/hosts` 
    - Di Windows file `c:\Windows\System32\Drivers\etc\hosts`, buka dengan notepad sebagai Administrator 
        


### Jika anda memilih menggunakan service mysql docker
  
  - Konfigurasi password di `services` `mysql` sepertinya cukup gampang dimengerti sekali lihat.

### Jika anda memilih menggunakan service mysql installan ada sendiri (agak ribet)
Ada kalanya anda malas merestore database lagi, konsekuensinya ya agak ribet sih.
  
  - Comment semua line pada `services` `mysql`.
  - Buat sql server anda supaya bisa diakses oleh ip dari service `meyaboo` dan `maxomorra`.

### Konfigurasi maxomorra dan meyaboo
sudah jelas

## Menjalankan docker
untuk pertama kali, atau setelah mengedit `docker-compose.yml` ketikkan `docker compose build`, setelah itu `docker-compose up`