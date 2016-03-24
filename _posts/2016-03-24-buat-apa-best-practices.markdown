---
layout: post
title:  "Buat Apa Best Practice?"
date:   2016-03-24
categories: keputusan teknologi
author: Edwin Lunando
author_t: edwinlunando
permalink: best-practice
header_image: /images/best_practice.png
---

Sejak pertama kali terjun di dunia perangkat lunak, ada sebuah pertanyaan yang selalu keluar dari mulut saya saat mengembangkan sebuah aplikasi.

*Untuk buat fitur ini, best practice-nya gimana ya?*

Dan segala varian dari pertanyaan tersebut yang intinya menanyakan *best practice* dari sebuah fitur, kasus, konfigurasi, atau metode. Tampaknya sudah tidak terhitung berapa kali saya menanyakan dan ditanyakan varian dari pertanyaan tersebut. Hingga akhirnya saya pun menutuskan untuk tidak membahas terkait *best practice* lagi sekarang. Kenapa?

## Penjelasannya Dangkal

Saya ingat sekali dulu saat pertama kali bikin aplikasi web, saya ingin menyimpan data pengguna termasuk dengan email dan password. Bikin fitur otentikasi pengguna sederhana. Saya bertanya ke temen saya yang lebih berpengalaman.

*Om, cara buat simpen data user enaknya gimana ya Om?*

Dijawab seperti ini

*Kalau password, best practice-nya di-hash dulu, kalau email dan data pribadi user simpen biasa aja*

Saat itu sih saya tentu saja menerima, toh sudah langsung dapet yang "best practice". Saya langsung saja ikutin langkah-langkah yang dia kasih tahu supaya mengikuti *best practice*. **Padahal, kan yang penting itu alasan dibalik *best practice* tersebut**. Yah saat itu sih saya belum dijelasin kenapa kalau menyimpang password itu harus di-[hash][4] dulu biar aman. Lama-lama setelah saya penasaran, akhirnya saya cari tahu sendiri kenapa menyimpan password tidak boleh teks biasa. Baru lah saya paham kenapa metode ini dilabeli *best practice*.

Karena mudah ngomong sesuatu ini *best practice*, akhirnya.

## Sering Dipakai Jadi Alasan

Beberapa waktu lalu, tim saya menemui masalah terkait [environment variable][0] yang ternyata setiap orang dan server tidak sinkron. Hasilnya, hasil di lokal dengan staging berbeda, menyebabkan proses pengembangan terhambat. Kondisinya tim kami sudah sebagian mengikuti metode yang dianggap *best practice*. Gak di-*push* ke repo, tiap orang punya file `.env` masing-masing, tiap server juga masing-masing. Saya usul.

*Gimana kalau kita pakai metode A, toh, aman juga selama pemakaiannya benar*

Rekan tim saya langsung menjawab.

*Metode A gak boleh, bukan best practice*

Huff. Diskusi berlanjut, pada akhirnya metodenya tidak diubah. Solusi yang dipilih akhirnya setiap orang diminta lebih *aware* terkait *environment variable*. Saya sih tidak masalah terhadap hasil akhirnya, tapi usul saya ditolak karena bukan *best practice*.

Saya masih punya bayak contoh yang baru saja saya sadari ternyata begitu banyak(termasuk saya) yang menggunakan alasan *best practice* ketika dihadapi dengan kejadian yang serupa.

**Kenyataannya *best practice* tidaklah selalu benar**. Belakangan ini, saya mengikuti rekomendasi *best practice* dari sebuah pustaka, hasilnya tidak terlalu memuaskan. Setelah saya coba korek-korek dalemannya, mencari tahu cara kerjanya, barulah saya tahu di mana letak kesalahannya dan memperbaikinya sendiri.

## Ujung-ujungnya Cara Kerja

Sejak saat itu, saya sadar kalau mengetahui cara kerja sebuah fitur, aplikasi, pustaka, atau metode itu jauh lebih penting daripada label *best practice*. Kelanjutan dari cerita password yang harus di-hash dulu itu, akhirnya saya [mencari tahu terkait beberapa fungsi hash yang aman digunakan untuk password][1]. Sekarang, sudah ada fungsi hash terbaru yang dinyatakan lebih aman dari yang disebut *best practice* sebelumnya. Namanya [argon2][2] dan fungsi hash ini langsung direkomendasikan banyak peneliti dan praktisi. Kenapa? Sok silahkan dibaca papernya di [sini][3].

Memang butuh kerepotan yang besar untuk memahami sesuatu, tapi **lebih baik saya repot sekarang daripada saya mengembangkan sebuah aplikasi tanpa tahu daleman yang saya gunakan atau implementasikan**. Toh kan katanya Peter Thiel

*Today’s “best practices” lead to dead ends; the best paths are new and untried.*

Selalu ada perbaikan atau inovasi baru dari *best practice* yang sekarang. :smile:

[0]:   https://en.wikipedia.org/wiki/Environment_variable
[1]:   {{ site.baseurl }}{% post_url 2015-01-14-cara-menyimpan-password %}
[2]:   https://github.com/P-H-C/phc-winner-argon2
[3]:   https://github.com/P-H-C/phc-winner-argon2/blob/master/argon2-specs.pdf
[4]:   https://en.wikipedia.org/wiki/Hash_function
[5]:   https://en.wikipedia.org/wiki/Peter_Thiel
