---
layout: post
title:  "Operasi Idempoten"
date:   2017-06-15
categories: produk wannacry
author: Edwin Lunando
author_t: edwinlunando
permalink: idempoten/
---

Akhirnya nulis teknis lagi! *Idempotent* menurut [kamus oxford][0] adalah.

> *Denoting an element of a set which is unchanged in value when multiplied or otherwise operated on by itself.*

Gua belum menemukan padanan bakunya, tapi sebut saja idempoten. Kalau di dunia pemrograman, intinya, sebuah operasi atau fungsi, kalau dijalankan lebih dari satu kali, hasilnya sama.

## Kasusnya

Baru di beberapa bulan ini gua membutuhkan sebuah fungsi hanya perlu dijalankan satu kali saja, tetapi karena ada kesalahan dari pengguna operasi tersebut dijalankan lebih dari satu kali yang menyebabkan duplikasi hasil.

Lebih detilnya, gua ingin mengirimkan sebuah pengumuman ke sejumlah pengguna. Tiap pengumuman ini unik dan tiap pengguna ini juga unik, tapi karena ada kesalahan pengguna, beberapa kali pengumumannya dikirim lebih dari satu kali ke tiap pengguna. Gak asik dong. Kita butuh solusinya untuk membuat fungsi ini idempoten.

## Solusi

Sederhana, kita butuh menyimpan sebuah penanda kalau sebuah pengumuman tersebut sudah dikirimkan ke pengguna tersebut. Selanjutnya, tiap kali mau mengirimkan pengumuman, kita melakukan pengecekan. Kalau belum ada tandanya untuk pengguna ini dan pengumuman ini, kirim. Kalau sudah ada, tidak dikirim.

Ini sejenis dengan semantik [*remote procedure call*][11]. Untuk kasus ini saya menggunakan yang *at most once*, paling banyak satu, karena setelah diukur nilai dari efeknya lebih bahaya duplikasi daripada tidak terkirim. Kami tidak masalah kalau ada sebagian kecil notifikasi yang tidak terkirim.

### Basis Data Relasional

Silakan pilih basis data relasional apa pun. Saya milih [MySQL][9]. Tiap kali melakukan pengiriman, kita log ke tabel yang kolomnya ada 2, yaitu `user_id` dan `notification_id`. Kira-kira begini lah.

| user_id       | notification_id   |
|:-------------:|:-----------------:|
| 7             | 18                |
| 1             | 13                |
| 2             | 12                |
| 3             | 12                |
| 1             | 12                |

Berfungsi! Tapi, kendalanya adalah performa. Di tabel contoh, isi kontennya hanya lima baris, kenyataannya, setiap hari kami mengirim pengumuman ke jutaan pengguna. Kecepatan pengiriman berkurang karena setiap pengiriman harus **mengecek semua penanda di tabel yang makin lama makin besar jumlah barisnya.**

{% highlight sql %}

# query ini memerlukan pengecekan ke semua elemen di tabel
select * from users_notifications where user_id = 1 and notification_id = 12

{% endhighlight %}

Toh, kompleksitasnya O(N). Solusi ini gak bisa digunakan di kasus kami. Lanjut ke pendekatan selanjutnya.

### Basis Data Relasional dengan Index

Sama seperti solusi sebelumnya, tapi ditambah dengan menggunakan fitur `index`. Dengan menggunakan indeks, kita akan secara otomatis membuat sebuah struktur data [B+ tree][7], sebuah struktur data yang dioptimasikan untuk operasi pencarian.

{% highlight sql %}

# bikin indeksnya
CREATE INDEX index_on_users_notifications ON users_notifications (user_id,notification_id);

# setelah dibuat indeksnya, query ini jadi hanya perlu menelusuri struktur data b+ tree
select * from users_notifications where user_id = 1 and notification_id = 12

{% endhighlight %}

Pakai [indeks komposit][8] karena ada dua kolom yang dijadikan patokan query. Jadi, kompleksitasnya O(log n). **Dengan mengorbankan sebagian ruang di tempat penyimpanan, kompleksitasnya nurun satu tingkat**. Emejing.

Cuma, yah, saya belum puas aja. Lanjut lagi pendekatan lain.

### Basis Data Kunci-Nilai

Maaf, padanan [*Key-value database*][1]-nya maksa. Saya memilih [redis][10] untuk basis data jenis ini. Kenapa pakai ini? Karena menggunakan struktur data [set][2] cocok untuk menaruh dan mengecek tanda pengiriman. Begini contohnya.

| Kunci         | Nilai             |
|:-------------:|:-----------------:|
| 7/18          | 1                 |
| 1/13          | 1                 |
| 2/12          | 1                 |
| 3/12          | 1                 |
| 1/12          | 1                 |

{% highlight sql %}
# masukkin nilai di kunci
> SADD '7/18' 1
"OK"

# pengecekan
> EXISTS '7/18'
"1"

> EXISTS '7/19'
"0"

{% endhighlight %}

Jadi, kuncinya itu terdiri dari teks `user_id/notification_id` dengan nilai apapun sebagai penanda. Tinggal ngecek kunci tersebut sudah ada isinya atau belum. Kalau sudah ada, tidak dikirim. Kalau belum, langsung kirim. Dengan kompleksitas [akses][5] dan [masukan][6] data rata-rata O(1), seharusnya pengaruh ke performa sangat minimal sampai tidak terasa. Apalagi mengingat kalau basis data kunci-nilai menaruh datanya di RAM. Performa bukan masalah.

Nah, [menurut redis][3], 1 juta kunci dan nilai sederhana itu menggunakan memori ~100MB. Saya kira-kira tiap hari itu mengirim pengumuman ke 5 juta pengguna. Jadi, setiap harinya, penggunaan memori server saya naik ~500MB. Satu minggu sudah naik ~3.5 GB. Masalah baru, nih!

### Basis Data Kunci-Nilai dengan Kedaluwarsa

Untungnya di redis, sudah ada fitur untuk menentukan waktu hidup dari sebuah kunci.

{% highlight sql %}
# masukkin nilai di kunci
> SADD '7/18' 1
"OK"

# tentukan waktu hidup kunci 1 minggu dalam detik
> EXPIRE '7/18' 604800
1

{% endhighlight %}

Sistem kedaluwarsa ini ampuh karena ternyata **hanya pengumuman yang baru-baru saja yang terduplikasi**. Terutama pengiriman di hari yang sama. Jadi, menghilangkan tanda pengiriman yang sudah beberapa hari yang lalu pun tidak masalah. Begini [cara redis menghapus kunci yang sudah kedaluwarsa][4].

Yak, metode yang terakhir yang sekarang sedang gua gunakan di server produksi. Kondisi sekarang pengiriman lancar dan tidak ada duplikasi lagi. Masalah selesai! Untuk sementara. Mungkin banget tiba-tiba nanti ada masalah baru entah dari bagian mana. Sekarang, kita tungguin dulu.

[0]:    https://en.oxforddictionaries.com/definition/idempotent
[1]:    https://en.wikipedia.org/wiki/Key-value_database
[2]:    https://redis.io/topics/data-types#sets
[3]:    https://redis.io/topics/faq
[4]:    https://redis.io/commands/expire#how-redis-expires-keys
[5]:    https://redis.io/commands/exists
[6]:    https://redis.io/commands/sadd
[7]:    https://en.wikipedia.org/wiki/B%2B_tree
[8]:    https://dev.mysql.com/doc/refman/5.7/en/multiple-column-indexes.html
[9]:    https://www.mysql.com/
[10]:   http://redis.io/
[11]:   https://web.cs.wpi.edu/~cs4514/b98/week8-rpc/week8-rpc.html
