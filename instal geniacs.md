INSTAL GENIACS

1. instal geniacs 

    🖋️docker --version 

     "Digunakan untuk memastikan Docker telah terpasang dengan benar serta menampilkan versi Docker yang sedang digunakan"

2. memeriksa apakah Docker Compose sudah tersedia dan menampilkan versi yang terinstal.

    🖋️docker compose version

3. Membuat direktori baru bernama genieacs-docker sebagai tempat menyimpan seluruh file instalasi GenieACS.

     🖋️mkdir genieacs-docker

4. Berpindah ke direktori genieacs-docker agar proses selanjutnya dilakukan di dalam folder tersebut.

     🖋️cd genieacs-docker

5. Membuka editor Nano untuk membuat atau mengedit file docker-compose.yml, yang nantinya akan diisi konfigurasi Docker Compose untuk menjalankan GenieACS.

     🖋️nano docker-compose.yml

6. lalu mengatur dan menjalankan seluruh layanan GenieACS dalam Docker secara otomatis.

   🖋️services:
   
  mongo:
  
    image: mongo:4.4
    
    container_name: genieacs-mongodb
    
    restart: always

    volumes:
    
      - mongo_data:/data/db

  redis:
  
    image: redis:7.0-alpine
    
    container_name: genieacs-redis
    
    restart: always
    
    volumes:
    
      - redis_data:/data

  genieacs-cwmp:
  
    build: .
    
    container_name: genieacs-cwmp
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
    ports:
    
      - "7547:7547"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-cwmp

  genieacs-nbi:
  
    build: .
    
    container_name: genieacs-nbi
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
    ports:
    
      - "7557:7557"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-nbi

  genieacs-fs:
  
    build: .
    
    container_name: genieacs-fs
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
    ports:
    
      - "7567:7567"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-fs

  genieacs-ui:
  
    build: .
    
    container_name: genieacs-ui
    
    restart: always
    
    environment:
    
      - GENIEACS_MONGODB_CONNECTION_URL=mongodb://mongo:27017/genieacs
      
      - GENIEACS_REDIS_CONNECTION_URL=redis://redis:6379/0
      
      - GENIEACS_UI_JWT_SECRET=rahasiasangat-aman-123
      
      - GENIEACS_UI_USERS=${GENIEACS_UI_USERS}
      
    ports:
    
      - "3000:3000"
      
    depends_on:
    
      - mongo
      
      - redis
      
    command: genieacs-ui

volumes:

  mongo_data:
  
  redis_data:
  
7. Jalankan seluruh layanan (service) GenieACS di latar belakang menggunakan Docker.

   🖋️sudo docker compose up -d

"Perintah ini berfungsi untuk menjalankan semua layanan GenieACS secara bersamaan berdasarkan konfigurasi yang ada pada file docker-compose.yml. Opsi -d membuat proses berjalan di latar belakang"

8. Cek status container yang sedang berjalan.

   🖋️sudo docker ps

"Perintah ini digunakan untuk melihat daftar container yang sedang aktif serta memastikan layanan GenieACS telah berhasil dijalankan"

9. Buka browser, lalu ketik

    🖋️http://192.168.115.2:3000
"Alamat tersebut digunakan untuk membuka halaman web GenieACS melalui browser menggunakan alamat IP server dan port 3000"

10. Jika berhasil masuk ke halaman GenieACS, klik ABRACADABRA

11. Masukkan username dan password yang disediakan oleh GenieACS.

    🖋️username : admin
    
    🖋️password : admin

12. Setelah login berhasil, akan tampil dashboard GenieACS.
