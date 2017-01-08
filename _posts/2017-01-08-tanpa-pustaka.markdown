---
layout: post
title:  "Tanpa Pustaka"
date:   2017-01-08
categories: pustaka desain
author: Edwin Lunando
author_t: edwinlunando
permalink: tanpa-pustaka/
---

Yey, desain baru! Sejak bulan lalu, gua pengen banget ganti desain blog ini karena setelah melihat banyak blog-blog lainnya, blog gue cupu banget dari sisi keterbacaan dan kecantikan. Nyaman banget baca tulisan di medium. Kalau dibandingin sama blog gue, dulu tuh awalnya gua dapet inspirasi [desain material][4] dari Google. Jadinya langsung gua ikutin tuh, sistem kartu, flat design, dan warna-warna yang cerah. Setelah kira-kira satu tahun mondar-mandir di blog orang lain, selalu balik ke desain di Medium. Oleh karena itu, ini desain baru blog gue. Dasar dan sederhana.

## Desain

Keterbacaan dan kompabilitas lintas peramban, itu 2 point yang menjadi fokus desain ulang dari blog ini. Mulai dari keterbacaan.
 
1. **Ukuran berpengaruh**. Sekarang resolusi layar sudah besar. Pilih ukuran minimal 16. Font ukuran kecil lebih cocok untuk media cetak.
1. **Kurangi kontras**. Sakit kan ngeliat kombinasi warna dengan tingkat kontras lebih tinggi dari monas? 
1. **Beri ruang untuk bernafas**. Kasian itu mata ngeliat jarak antar baris rapet banget.
1. **Cukup per satu halaman**. Satu baris cukup 80 karakter biar bacanya lancar dari atas ke bawah.

Situs ini dibuat dengan CSS yang sangat minimal(200 baris) dan ternyata sudah responsif di perangkat yang layarnya kecil maupun besar tanpa menggunakan [media query][2]. Dibuka di berbagai jenis peramban pun sama. Silahkan dicoba.  :wink:. Kata siapa butuh media query supaya bisa responsif?

## Kecepatan

Gua mau blog ini jauh lebih ringan dari yang sebelumnya. Ini hasilnya. Di halaman depan, dibandingakan dengan desain yang sebelumnya,

1. Dari 17 HTTP *request* ke 4 *request*.
1. Dari 400KB ke 40KB
1. [Tanpa javascript sama sekali][5], cuma HTML dan CSS.

Saat gua nyari inspirasi buat desain baru ini, gua riset banyak pustaka CSS dan Javascript seperti [Bootstrap][3], salah satu yang legendaris, tapi ukuran CSS-nya yang versi *minified*-nya aja lebih dari 100KB. Untuk ngasih animasi sedikit, perlu nambahin 80KB Jquery ditambah dengan javascript Bootstrap-nya sendiri. Mau nambah beberapa ikon media sosial, nambah lagi font awesome yang ukurannya mencapai 100KB-an. **Padahal, konten teks dari blog, biasanya gak lebih dari 20KB**. Pantesan ya peramban butuh memory yang gede. Jadi, tidak untuk Bootstrap.
   
Riset gua berlanjut. Okelah gua gak perlu pustaka yang berat-berat, jadi, pencarian gua fokus ke pustaka ringan yang buat layout saja. Ketemu [Skeleton][0] dan [Flexbox grid][1]. Tapi, setelah dipikir-dikir lagi, sebenernya pun gua gak butuh sistem layout. Toh, blog gua paling ada 2 sampai 4 tipe halaman dan kebanyakan cuma konten linier dari atas ke bawah saja. Jadi, pada akhirnya, gua memutuskan untuk untuk tidak pakai pustaka apapun. Ada begitu banyak pisau yang bisa kita pilih, tapi untuk kasus ini, saya memutuskan untuk tidak menggunakan pisau.

## Hasilnya

Gua puas banget, sekarang baca blog gua sendiri lebih cantik dan nyaman, cepat pula. Tapi, tentu saja belum sempurna. Ini baru iterasi pertama. Masih ada elemen desain seperti gambar yang gua yakin bisa mempercantik blog ini. Tunggu saja perkembangan selanjutnya!
 
[0]:    http://getskeleton.com/
[1]:    http://flexboxgrid.com/
[2]:    https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries
[3]:    http://getbootstrap.com/
[4]:    https://material.io/guidelines/
[5]:    https://meta.discourse.org/t/the-state-of-javascript-on-android-in-2015-is-poor/33889
