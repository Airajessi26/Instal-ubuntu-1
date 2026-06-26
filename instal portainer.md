instal portainer

1.membuat sebuah Docker Volume yang diberi nama portainer_data.
  Volume adalah tempat penyimpanan data permanen yang dikelola oleh Docker.

 🖋️docker volume create portainer_data

2. menginstal sekaligus menjalankan Portainer sebagai container Docker.
   Setelah berhasil dijalankan, Portainer dapat diakses melalui browser dengan alamat: https://IP-Server:9443

  🖋️docker run -d \ -p 8000:8000 \ -p 9443:9443 \ --name portainer \ --restart=always \ -v /var/run/docker.sock:/var/run/docker.sock \ -V
  portainer_data:/data \ portainer/portainer-ce:latest

3. melihat daftar container Docker yang sedang berjalan (running).
    
  🖋️docker ps

4. Tekan Enter untuk membuka halaman Portainer. Jika muncul peringatan keamanan karena menggunakan sertifikat bawaan (self-signed certificate),          pilih Advanced/Lanjutan lTekan Enter untuk membuka halaman Portainer.
     "Tekan Enter untuk membuka halaman Portainer. Jika muncul peringatan keamanan karena menggunakan sertifikat bawaan (self-signed certificate),          pilih Advanced/Lanjutan lalu Proceed/Lanjutkan agar dapat masuk ke halaman Portainer"

  🖋️https://192.168.1.100:9443

