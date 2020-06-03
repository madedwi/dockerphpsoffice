Docker-compose untuk keperluan DMS App

# Installasi
1. Clone repositori ke lokal
2. Rename docker-compose.yml.example -> docker-compose.yml
3. Setting host path yang akan di mount ke container pada docker-compose.yml
4. Jalankan command build 
5. Jalankan command up

# Database setting
1. Gunakan 172.17.0.1:3306 sebagai DSN pada database config.
2. Grand access root@128.0.0.2 pada database


Reff : 

[Install Docker Windows](https://docs.docker.com/docker-for-windows/install/)

[Install Docker Compose](https://docs.docker.com/compose/install/)
