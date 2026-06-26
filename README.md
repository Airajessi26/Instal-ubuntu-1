●Login ke Ubuntu
 •masukan username
 •masukan password
 masuk kesisitim ubuntu
●Memperbarui daftar paket
 •sudo apt update
●menampilkan daftar paket yang memiliki pembaruan (update) dan siap di-upgrade.
 •sudo apt list --upgradable
●memperbarui paket-paket yang sudah terinstal di Ubuntu, kemudian mengecek apakah masih ada paket yang belum diperbarui.
 •sudo apt upgrade && sudo apt upgradable
 • lalu y untuk yes
●membersihkan instalasi Docker yang lama atau paket lain yang bisa menyebabkan konflik,
 •for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc;
  do sudo apt-get remove $pkg; done
●mengunduh (download) skrip instalasi Docker resmi dari situs Docker dan menyimpannya ke file bernama get-docker.sh.
 •curl -fsSL https://get.docker.com -o get-docker.sh
●menampilkan daftar file dan folder dalam format lengkap (long listing) pada direktori saat ini.
 •ls -l
●menjalankan skrip instalasi Docker 
 •sudo sh get-docker.sh
●menampilkan informasi versi Docker yang terpasang
 •docker version
●menguji apakah Docker sudah terinstal dan berfungsi dengan baik.
 •docker run hello-world
