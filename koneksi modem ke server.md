koneksi modem ke server

1. siapkan alat alat

   a. modem 

   b. spliter

   c. cabel fo singel mode

   d. koneksi internet

   e. hp / leptop

   f. adaptor modem

   g. stopkontak

2. nyalakan modem

   a. hbungkan adapter modem ke setop kontak

   b. sambungkan kabel fo ke spliter dan ujung satunya ke modem

   c. sambungkan lagi kacel fo dari spliter ke modem

3. seting modem

   a. koneksikan dengan wifi sesuaimodem yang akan di seting

   b. buka browser dan ketik ip yang sesui dimodem

   c. lalu isi usernam dan pasword

4. klik pada menu dasbord  -> network -> wan lalu setig

    Enable VLAN ✅

    Vlan ID    514

    Service List : TR069VOIP-INTERNET

   Username : acs-pkl

   Pasword : acs-pkl

   Port Binding ✅LAN1  ✅LAN2 ✅LAN3 ✅LAN4

                ✅SSID1

  a. jika sudah menyeting semua lalu klik create

  b. masih pada menu network -> WLAN -> Seting pada Aauthenticatin Type:Open System -> submit

  c. ke menu dasbord pilih menu status ->interface network 

   pastikan ip address dan DNS sudah ada ip dan conneted
  
  d.buka aplikasi speestest ->mulai -> akan mucul redaman dan mbps nya bererti seting modem telah berhasil

5. Buka aplikasi Winbox, pada halaman login winbox masukkan IP yang terhubung ke port ONT (contoh: 103.134.220.123:12500) -> connect

6. pilih menu ppp -> active connections -> ketik acs-pkl pada kolom pencarian -> kilik 2 kali -> copy paste IP Addnya di browser ->enter

7. Setelah masuk ke halaman login setting modem masukkan username dan passwordnya -> login

8. Pilih menu administration -> TR09 
