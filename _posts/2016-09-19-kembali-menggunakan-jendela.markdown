---
layout: post
title:  "Kembali Menggunakan Jendela"
date:   2016-09-19
categories: windows back using
author: Edwin Lunando
author_t: edwinlunando
permalink: kembali-menggunakan-jendela
---

Yak, setelah sekian lama mengembara menggunakan [Linux][0]([Ubuntu][1], [Kubuntu][2]) dan [Mac][3](Sebenernya OS X atau macOS, tapi saya sebutnya Mac aja ya), saya akhirnya memutuskan untuk kembali menggunakan [Windows][4] sebagai sistem operasi utama saya. Selain dua alasan klasik untuk pengguna Windows(Microsoft Office dan Gaming), saya punya beberapa alasan yang buat saya penting krusial yang memengaruhi kenyamanan dan produktifitas saya dalam bekerja atau pun bermain. Langsung saja, yuk!

## Pengalaman Navigasi

Yak, saya paling suka navigasi Windows. Contoh yang paling penting buat saya adalah navigasi antar aplikasi. alt-tab di Windows instan dan efisien. Dari awal tekan alt-tab, lalu saya bisa memilih window dengan tombol panah saya. Di Linux, saya tidak pernah mendapatkan pengalaman instan. Selalu ada delay beberapa puluh milidetik, dengan spesifikasi kemampuan komputer yang sama. Di Mac, navigasi saat *full-screen*-nya harus banget pake animasi, gak bisa instan juga. Pencarian utama dalam sistem operasinya pun tidak seinstan Windows.

**Buat saya yang fokusnya kecepatan dan produktivitas, navigasi instan itu tidak bisa ditawar**. Ada delay beberapa puluh sampai ratusan mili detik, buatku sangat berpengaruh. Bahkan, saya sendiri sudah [tidak tahan kalau komputer yang saya gunakan masih menggunakan SSD][5].

## Driver And App Support

Pengalaman saya kalau beli laptop, terus di-install-in Linux, selalu saja ada masalah perangkat yang tidak berjalan dengan baik. Entah itu *keyboard*, *touchpad*, *wireless LAN*, dan kartu grafis. Saya tidak pernah mengalami hal ini di Mac dan jarang sekali di Windows. Dulu pas masih belajar terkait daleman sebuah sistem operasi sih seru-seru aja eksplorasi sendiri untuk benerin yang rusak. Sekarang, maunya lebih fokus ke yang lebih produktif.

Yang tak kalah penting juga adalah jumlah aplikasi ber-GUI! **Walaupun keseharian saya sebagai insinyur perangkat lunak ini menggunakan konsol atau terminal secara intensif, aplikasi yang ada GUI-nya sangat membantu di banyak kasus**. Linux jumlah aplikasi ber-GUI-nya relatif lebih sedikit daripada Mac dan Windows. Saat pakai Linux, ujung-ujungnya tab peramban saya bakal sangat banyak karena menggunakan aplikasi versi web-nya. Tapi, jelas kalau kita bicara soal aplikasi server yang biasa digunakan dalam pengembangan aplikasi, Linux tidak tergantikan.

## Windows Semakin Memanjakan Developer

Sejak baru-baru ini, Windows mulai banyak fitur-fitur yang membantu *engineer* dalam pekerjaan mereka. Contohnya, virtualisasi native hyper-v, *command line* berbasis Linux, dan .NET sekarang sudah tidak eksklusif Windows. Fitur-fitur tersebut memang belum matang, tapi arahnya semakin pro engineer. Itu yang aku suka.

## Gak Enaknya Windows

Udah sistem operasi berbayar, masih dikasih iklan juga. :(. Di beberapa halaman, dapet "*Suggested app*". Pas install Windows, ternyata sudah di-install-in gim kayak Candy Crush Saga. Tentunya semuanya bisa dihapus dan di-nonaktifkan, tapi rese aja dikasih iklan terus, gak relevan lagi.

Windows update! Windows sering bareng ngasih update yang wajib. Mau restart, disuruh update. Mau matiin, disuruh update juga. Yah, sisi plus-nya sih sistem operasinya jadi selalu yang terbaru, tapi ya, ngeselin aja, pas udah mau pulang, eh, kehambat harus update dulu.

Untuk engineer yang kerjanya butuh lingkungan Linux, terpaksa virtulisasi. Entah itu pakai [VirtualBox][6] atau [Hyper-V][7]. Selama ini sih saya pakai VirtualBox dengan [Vagrant][8]. Dalam waktu dengan akan mencoba Hyper-V. Kalau sudah bicara virtualisasi, tentunya ada sebagian performa yang dikorbankan. Sampai sekarang delay yang ada dengan menggunakan virtualisasi masih dapat saya toleransi sih.

## Titik Terang

Jadi, yak, sebenernya tidak ada satu fitur bener-bener mantep yang bikin aku langsung mau pake Windows. Semua berawal dari fitur-fitur kecil yang ternyata setelah dibandingkan, lebih asik dan bikin produktif daripada sistem operasi lain. Windows merupakan sistem operasi pertama saya sejak sekolah dasar, mulai pakai Linux semenjak di kampus, dan Mac pas kerja.

Saya punya banyak pengalaman buruk dalam menggunakan Linux, mulai dari ada hardware yang tidak jalan sampai dengan aplikasi tiba-tiba *crash* sendiri. Sulit untuk saya kembali ke Linux kalau tidak ada perubahan yang berarti. Untuk Mac, saya sebenernya hanya sedikit masalahnya dan kebanyakan minor, saya mau saja kok menggunakan Mac. Toh, basisnya Unix juga, pastinya nyaman dengan lingkungan pengembangan Unix ditambah dengan suppport aplikasi yang melimpah. Tapi, tetep sih, **gak ada yang ngalahin alt+tab kerja-game dan pengalaman navigasi instan di Windows**. :)

[0]:    https://en.wikipedia.org/wiki/Linux
[1]:    http://www.ubuntu.com/
[2]:    http://www.kubuntu.org/
[3]:    https://en.wikipedia.org/wiki/OS_X
[4]:    https://en.wikipedia.org/wiki/Microsoft_Windows
[5]:    {{ site.baseurl }}{% post_url 2015-11-25-pakai-ssd-atau-kehilangan-produktivitas %}
[6]:    https://www.virtualbox.org/
[7]:    https://www.microsoft.com/en-us/cloud-platform/virtualization
[8]:    https://www.vagrantup.com/
