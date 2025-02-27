---
layout: page
title: Modul 1
parent: Modul
permalink: /modul/modul-1/
---
Modul ini mencakup proses instalasi dari seluruh komponen yang diperlukan untuk modul 2, yang juga digunakan pada modul 3

## Instalasi Git

  ```bash
  sudo apt install git
  ```
# Instalasi sraRAN
Sebelum melakukan penginstalan srsRAN, jalankan kode berikut untuk menginstal depencencies
  ```bash
  sudo apt-get install build-essential cmake libfftw3-dev libmbedtls-dev libboost-program-options-dev libconfig++-dev libsctp-dev
  ```
## Instalasi ZeroMQ
Instalasi RF Driver ZeroMQ perlu dijalankan di awal agar proses building dari srsRAN dapat berjalan lancar

Di Ubuntu, library ZMQ dapat diinstal menggunakan command berikut
  ```bash
  sudo apt-get install libzmq1-dev
  ```
Instalasi dari source juga dapat dilakukan menggunakan cara berikut
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
Jangan lupa untuk kembali ke folder /home/praktikum5g agar file yang di clone akan tersimpan pada folder home/user
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
  sudo make install
  sudo su
  srsran_install_configs.sh user # untuk menginstall file konfigurasi pada /root/.config/srsran/
  exit
  ```
