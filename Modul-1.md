---
layout: page
title: Modul 1
parent: Modul
permalink: /modul/modul-1/
---
Modul ini mencakup proses instalasi dari seluruh komponen yang diperlukan untuk modul 2, yang juga digunakan pada modul 3
## Instalasi srsRAN
Sebelum melakukan penginstalan srsRAN, jalankan kode berikut untuk menginstal depencencies
```bash
sudo apt install git libtool curl gnupg ca-certificates
```
```bash
sudo apt-get install build-essential cmake libfftw3-dev libmbedtls-dev libboost-program-options-dev libconfig++-dev libsctp-dev
```
### Instalasi ZeroMQ
Instalasi RF Driver ZeroMQ perlu dijalankan di awal agar proses building dari srsRAN dapat berjalan lancar

Di Ubuntu, library ZMQ dapat diinstal menggunakan command berikut
```bash
sudo apt-get install libzmq3-dev
```
Instalasi dari source juga dapat dilakukan menggunakan cara berikut, namun **kurang disarankan**
Instalasi libzmq
```bash
git clone https://github.com/zeromq/libzmq.git
cd libzmq
./autogen.sh
./configure
make
sudo make install
sudo ldconfig
```
Kembali ke folder /home/praktikum5g agar file yang di clone tidak masuk folder libzmq dengan menggunakan command berikut
```bash
cd ~
```
atau
```bash
cd ..
```
atau
```bash
cd /home/praktikum5g
```
Instalasi czmq
```bash
git clone https://github.com/zeromq/czmq.git
cd czmq
./autogen.sh
./configure
make
sudo make install
sudo ldconfig
```
Jangan lupa untuk kembali ke folder /home/praktikum5g agar file yang di clone akan tersimpan pada folder home/user. \n
**Sebelum install srsRAN, proses install driver BladeRF perlu dilakukan agar bisa di recognize sama srsRAN nya**
**hal ini tidak diperlukan pada praktikum ini karena penggunaan SDR tidak akan dilakukan pada VM pada modul 1 dan 2**
### Instalasi Driver BladeRF
Di Ubuntu, proses instalasi dapat dilakukan dengan menggunakan Personal Package Archives sebagai berikut
```bash
sudo add-apt-repository ppa:nuandllc/bladerf
sudo apt-get update
sudo apt-get install bladerf
```
Driver BladeRF sudah terinstal, namun jangan lupa untuk install firmware dan image FPGA yang dapat dilakukan menggunakan command berikut
```bash
sudo apt-get install bladerf-firmware-fx3     # firmware untuk semua model bladeRF
sudo apt-get install bladerf-fpga-hostedx40   # FPGA image untuk bladeRF x40
sudo apt-get install bladerf-fpga-hostedx115  # FPGA image untuk bladeRF x115
sudo apt-get install bladerf-fpga-hostedxa4   # FPGA image untuk bladeRF 2.0 Micro A4
sudo apt-get install bladerf-fpga-hostedxa9   # FPGA image untuk bladeRF 2.0 Micro A9
```
**Masing-masing jenis bladeRF dapat dilihat pada bagian FPGA dengan contoh sebagai berikut**
![BladeRF x115](/images/x115_c_new.png)
### Instalasi srsRAN_4G
Selanjutnya, akan dilakukan instalasi srsRAN_4G dengan command berikut
```bash
git clone https://github.com/srsRAN/srsRAN_4G.git
cd srsRAN_4G
mkdir build
cd build
cmake ../
```
Perhatikan keluaran command cmake ../ untuk memastikan bahwa ZeroMQ terbaca oleh srsRAN
```bash
-- FINDING ZEROMQ.
-- Checking for module 'ZeroMQ'
--   No package 'ZeroMQ' found
-- Found libZEROMQ: /usr/local/include, /usr/local/lib/libzmq.so
```
Bila ditemukan, lanjutkan proses instalasi ke tahap berikut
```bash
make
make test
```
**Apabila ada hasil yang gagal/error pada proses make test, ulangi proses dengan menggunakan command berikut**
```bash
ctest --rerun-failed
```
bila sudah berhasil, bisa dilanjutkan menggunakan command berikut
```bash
sudo make install
sudo su
srsran_install_configs.sh user # untuk menginstall file konfigurasi pada /root/.config/srsran/
exit
```
## Instalasi Open5GS
Sebelum menginstal Open5GS, akan dilakukan penginstalan MongoDB terlebih dahulu sebagai berikut
### Instalasi MongoDB
Pertama, akan dilakukan pengambilan GPG key untuk menginstal MongoDB
```bash
sudo apt update
curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor
```
Selanjutnya akan dibuat file list /etc/apt/sources.list.d/mongodb-org-6.0.list untuk versi Ubuntu yang digunakan. VM yang digunakan ialah Ubuntu 22.04, sehingga command yang digunakan adalah sebagai berikut.
```bash
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```
Selanjutnya, tinggal lakukan instalasi package MongoDB
```bash
sudo apt update
sudo apt install -y mongodb-org
sudo systemctl status mongod
sudo systemctl start mongod # lakukan bila mongod belum jalan
sudo systemctl enable mongod # untuk memastikan MongoDB berjalan setiap booting
```
### Instalasi Open5GS
Di Ubuntu, proses instalasi dapat dilakukan dengan menggunakan Personal Package Archives sebagai berikut
```bash
sudo add-apt-repository ppa:open5gs/latest
sudo apt update
sudo apt install open5gs
```
### Instalasi Open5GS GUI
Untuk GUI Open5GS, diperlukan penginstalan node.js terlebih dahulu yang dapat dilakukan menggunakan command berikut
Berikut command untuk mengambil GPG key
```bash
sudo apt update
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
```
Meembuat repository
```bash
NODE_MAJOR=20
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
```
Instalasi nodejs
```bash
sudo apt update
sudo apt install nodejs -y
```
Terakhir, GUI Open5GS dapat diinstal menggunakan command berikut pada sistem Ubuntu/Debian
```bash
curl -fsSL https://open5gs.org/open5gs/assets/webui/install | sudo -E bash -
```
### Selesai deh modul 1, tinggal lanjut ke modul 2 untuk tahap konfigurasinya yah :D
### SEMANGAT!!!
