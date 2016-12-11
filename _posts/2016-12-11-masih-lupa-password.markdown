---
layout: post
title:  "Masih Lupa Sandi?"
date:   2016-12-11
categories: sandi manajemen-sandi aplikasi
author: Edwin Lunando
author_t: edwinlunando
permalink: lupa-sandi/
---

Coba hitung jumlah aplikasi yang kamu gunakan, berapa banyak yang membutuhkan kata sandi? Tiap ada aplikasi baru, daftar, artinya sandi baru juga. Kalau terus menerus menggunakan sandi yang sama, sekalinya bobol, langsung deklarasi bangkrut. Kalau tiap aplikasi menggunakan sandi yang berbeda-beda, ngingatnya gimana? Taruh di dokumen, nanti bisa keliatan orang lain. [Bikin sandi yang pendek, nanti gampang di *brute-force* dengan kondisi prosesor komputer yang semakin cepat][2]. Ndak mau kan hadepin masalah-masalah tersebut untuk sisa hidupmu? Masa gaya hidup digital ini masih lumayan lama lah. Sebelum ada [metode otentikasi lain][1] yang jadi standar, solusinya pakai aplikasi manajemen sandi.

## Cukup Ingat 1 Sandi

Secara teori, kamu cuma cukup mengingat, menulis, atau menyimpan satu buah sandi, untuk mengakses semua sandi kamu. Mungkin kita bisa bilang bisa jadi lebih berbahaya karena kalau akun ini jebol, semua akun lain juga jebol. Oleh karena itu, aplikasi menejemen sandi punya beberapa fitur yang memperkuat satu pintu ini seperti:

1. Kunci keamanan: Selain sandi, untuk mengakses akun dibutuhkan kunci yang bisa berupa teks atau berkas.
2. Otentikasi ponsel: Kita bisa menggunakan ponsel kita untuk mengotentikasi setiap permintaan login.
3. Verifikasi email: Tiap kali login di device lain, perlu konfirmasi email.

Selama penggunaannya benar, dengan menggunakan salah satu dari fitur harusnya sudah aman. Saya sendiri mengggunakan otentikasi ponsel karena saya lebih nyaman menggunakan [aplikasi otensikasi][3] di ponsel saya.

## Pembuatan sandi otomatis

Gak usah mikir buat bikin sandi yang panjang nan susah ditebak sama komputer. Ini fitur wajib yang selalu ada di aplikasi manajemen sandi manapun. Pastikan saja panjang sandinya di atas 12(relatif cukup aman untuk jaman sekarang). Beberapa tahun lagi mungkin perlu ditambah saat ada lompatan pengembangan di teknologi prosesor. :sunglasses:

## Kemudahan Akses

Hampir semua aplikasi manajemen sandi yang populer mempunyai akses web dan aplikasi ponsel. Sebagian mempunyai aplikasi desktop. Intinya, **dalam kondisi ada koneksi internet atau tidak, kamu bisa mengakses sandi-sandi kamu**. Koneksi internet digunakan untuk sinkronisasi sandi yang terbaru.

## Pasti Aman?

Perlu diketahui bahwa penggunaan aplikasi manajemen sandi ini bukan berarti aman secara absolut, karena tidak ada keamanan yang absolut. Tapi, aplikasi manajemen sandi ini sudah solusi yang jauh lebih baik dari alternatif yang lain seperti mengingat banyak sandi, mencatat sandi lalu menyembunyikan di laci atau bawah bantal, atau bahkan ditaruh di berkas digital. Dannnnn, kenyataannya, aplikasi manajemen sandi ini mungkin saja diretas. Yang paling terkenal itu [lastpass.com(aplikasi manajemen sandi) diretas pada tahun 2015][4]. Untungnya, teknologi sekarang membuat kalaupun datanya diretas dan diambil, minimal sandi-sandi kamu akan tetap aman karena sudah [dienkripsi][5].

## Bukan Solusi Nyaman

Untuk rekomendasi, saya menggunakan [1password][6] dan [lastpass][7](masih mencoba keduanya). Yah, saya tahu mengurus sandi bukan kegiatan yang nyaman, tapi kalau dipikirkan lebih lanjut terkait efeknya kalau lupa sandi atau kehilangan akses ke akun-akun digital kita, sebanding lah dengan usaha yang kita lakukan. Pernah kan ketemu kasus atau bahkan mengalami kehilangan akses ke akun digital? Horor, gan. Aplikasi ini bukan *silver bullet*. Tetap saja semakin banyak sandi yang kita punya, semakin capek juga mengurusnya. Aplikasi ini membuat mengurus sandi lebih manusiawi. :wink:

[0]:    https://en.wikipedia.org/wiki/Brute-force_attack
[1]:    http://newatlas.com/three-alternatives-passwords/31695/
[2]:    https://xkcd.com/936/
[3]:    https://play.google.com/store/apps/details?id=com.google.android.apps.authenticator2&hl=en
[4]:    https://blog.lastpass.com/2015/06/lastpass-security-notice.html/
[5]:    https://en.wikipedia.org/wiki/Encryption
[6]:    https://1password.com/
[7]:    http://lastpass.com/
