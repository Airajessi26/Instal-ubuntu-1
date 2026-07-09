setelah seting modem telah selesai, langkah berikutnya koneksikan genieACS ke modem untuk melakukan menejemen jarak jauh secara terpusat 

1. pastikan komputer atau leptop yang digunakan telah terhubung ke jaringan modem
   
3. sebelumnya buat "cwmp.connectionRequestAuth" agar nantinya bisa terhubung (summon)

   🖋️ admin >config >new config lalu

   🖋️ isi key dengan (cwmp.connectionRequestAuth)

   🖋️ alu isi value dengan (AUTH("admin", "admin")
   
5. Buka aplikasi Winbox, pada halaman login winbox masukkan IP yang terhubung ke port ONT (contoh: 103.134.220.123:12500) -> connect

6. pilih menu ppp -> active connections -> ketik acs-pkl pada kolom pencarian -> kilik 2 kali -> copy paste IP Addnya di browser ->enter

7. Setelah masuk ke halaman login setting modem masukkan username dan passwordnya -> login

8. Pilih menu administration -> TR069 Pada kolom ACS URL, masukkan alamat GenieACS. Jika sebelumnya menggunakan port 3000, ubah menjadi 7547 (contoh: http://192.168.115.2:7547). Pastikan fitur Enable dalam keadaan aktif.

9. 6. Isi Username dengan admin dan Password dengan admin, kemudian klik Submit atau Apply untuk menyimpan pengaturan.

10. Kembali ke halaman GenieACS, lalu pastikan modem telah terdeteksi dan berhasil terhubung

11. Jika modem sudah muncul di GenieACS, tekan tombol Summon untuk memaksa modem mengambil konfigurasi terbaru dan memperbarui data parameter tanpa menunggu proses otomatis.

12. Apabila status berubah menjadi "Summoned", berarti modem telah berhasil terhubung dengan GenieACS dan proses konfigurasi berjalan dengan baik tanpa kendala.
    
13. 
