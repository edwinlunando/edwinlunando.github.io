---
layout: post
title:  "Operasi Idempoten"
date:   2017-05-19
categories: produk wannacry
author: Edwin Lunando
author_t: edwinlunando
permalink: idempoten/
---

Akhirnya nulis teknis lagi! *Idempotent* menurut [kamus oxford][0] adalah.

    Denoting an element of a set which is unchanged in value when multiplied or otherwise operated on by itself.

Gua belum menemukan padanan bakunya, tapi sebut saja idempoten. Intinya, sebuah operasi atau fungsi, kalau dijalankan lebih dari satu kali, hasilnya sama.

## Kasusnya

Baru di beberapa bulan ini gua membutuhkan sebuah fungsi hanya perlu dijalankan satu kali saja, tetapi karena ada kesalahan dari pengguna operasi tersebut dijalankan lebih dari satu kali yang menyebabkan duplikasi hasil.

Lebih detilnya, gua ingin mengirimkan sebuah pengumuman ke sejumlah pengguna. Tiap pengumuman ini unik dan tiap pengguna ini juga unik, tapi karena ada kesalahan pengguna, beberapa kali pengumumannya dipublikasinya lebih dari satu kali ke tiap pengguna. Gak asik dong. Kita butuh solusinya untuk membuat fungsi ini idempoten.

## Solusi

### Database Relasional

Sederhana, gua tiap kali melakukan pengiriman, gua log ke tabel yang kolomnya ada 2, yaitu `user_id` dan `notification_id`. Kira-kira begini lah.

TODO tabel users_notifications

### Database Relasional dengan Index


### Key Value Database


### Key Value Database dengan Expire





[0]:    https://en.oxforddictionaries.com/definition/idempotent
