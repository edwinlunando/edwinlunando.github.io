---
layout: post
title:  "Keputusan Teknologi"
date:   2016-02-23
categories: keputusan teknologi
author: Edwin Lunando
author_t: edwinlunando
permalink: keputusan-teknologi/
header_image: /images/keputusan_teknologi.png
---

Akhir-akhir ini saya banyak ditanya terkait pemilihan *web framework*, basis data, aplikasi, dan pustaka. Saya dulu juga sering bertanya "Kenapa sih pake teknologi A? Kan ada B juga nih?" ke setiap orang. Hasilnya, gak ada aturan yang ketat dalam pemilihan teknologi. Kenyataannya, pemilihan teknologi sangatlah subjektif. Sangat tergantung dari orang yang bersangkutan dan kondisi saat itu. Ada yang memilih karena sudah lama dia gunakan, ada yang memilih karena dia senang menggunakan teknologi tersebut, ada yang milih karena itu teknologi terbaru, dan berbagai macam alasan lainnya.

Berikut merupakan hal-hal yang saya pertimbangkan saat mengambil keputusan teknologi beserta kasus-kasus yang saya temukan di dunia pemilihan teknologi. Karena saya seorang *backend engineer* yang suka dengan bahasa pemrograman dinamis, yah, kira-kira kebanyakan kasusnya akan seputar itu. Tapi, aturan-aturan umum yang saya buat ini berlaku di setiap teknologi yang saya pilih, tidak terkecuali di dunia *backend*.

## Kemampuan

Saya sudah mampu menggunakan teknologi ini belum? Ya, kalau saya sudah pernah menggunakan atau piawai dalam menggunakan teknologi tersebut, tentu saja ini menjadi alasan yang sangat valid untuk memilih teknologi tersebut, terutama dalam sebuah startup yang mempunyai sumber daya sangat terbatas. **Kalau milih teknologi yang belum dikenal, nanti waktunya habis eksplorasi daripada membangun aplikasi**. Ditambah lagi kalau menggunakan teknologi kekinian yang belum banyak diadaptasi, saat ingin menambah *engineer*, butuh waktu dan biaya untuk melatihnya.

Biasanya saya menggunakan teknologi baru pada saat eksplorasi atau proyek pribadi. Kalau ingin bikin startup yang fokusnya lebih ke *get things done*, saya memilih teknologi yang sudah saya kenal baik.

## Waktu

Kalau memang deadline yang diberikan itu mepet, tentunya saya akan memillih teknologi yang pragmatis cepat pengerjaannya. Kondisinya, saya cukup mumpuni menggunakan Django dan Rails, tapi kualitas Rails sebagai *framework web* lebih baik daripada Django(pendapat pribadi, bukan mau memulai perang dunia) :laughing:. Jika saya kalau diberikan pilihan, saya pasti memilih Django karena saya senang menggunakan Python, tapi jika waktu menjadi batasan, menggunakan Rails akan selesai lebih cepat.

## Kondisi Teknologi

Sebuah teknologi bisa kalaluarsa kalau tidak diurus dengan baik. Berikut beberapa persyaratan pribadi saya saat memilah teknologi. Entah itu sebuah *framework*, *library*, atau aplikasi.

1. **Tim yang aktif dalaman menangani teknologi tersebut**. Artinya, pengembangan selalu berjalan dan ada tim yang siap mengatasi kalau ada masalah yang terkait dengan teknologi tersebut.
2. **Komunitas yang peduli dengan teknologi tersebut**. Di saat kita menghadapi masalah dengan teknologi yang kita pakai, dukungan komunitas merupakan salah satu faktor yang menentukan seberapa cepat masalah itu akan selesai. Contohnya, saya memakai MySQL yang sudah berumur puluhan tahun dengan komunitas yang sangat besar. Saat saya menemukan masalah, ada kemungkinan yang sangat besar kalau ada orang lain yang sudah terkena masalah yang sama dan sudah punya solusinya. Kemewahan yang tidak dapat kita temukan di teknologi yang kekinian.
3. **Dokumentasi yang super lengkap(dan benar)** :sweat_smile:. Percayalah, menggunakan pustaka tanpa dokumentasi mirip dengan menyusun mebel IKEA tanpa buku petunjuknya. Bisaaaaaaaaa, tapi lebih susah, makan waktu dan energi lagi.

## Pendukung Teknologi

Tidak ada pustaka yang bisa berdiri kokoh tanpa bantuan dari pustaka-pustaka pendukung lainnya. Kalau mau memilih sebuah teknologi, saya juga memperhitungkan kuantitas dan kualitas dari pustaka pendukungnya. **Inilah kasus nyata dengan Rails. Rails mempunyai *third-party library* yang sangat banyak dan masih di-*maintain* dengan baik**. Pengalaman saya menggunakan framework lain(Django dan Laravel), jumlah pustakanya tidak sebanyak Rails dan beberapa pustaka yang krusial sudah tidak di-*maintain* dengan baik.

## Jumlah Pengguna Lokal

Kalau sebuah teknologi bagus, tapi tidak ada pengguna lokal yang menggunakannya juga bisa menjadi faktor pertimbangan. Jika pada saatnya sebuah tim akan berkembang, tentunya lebih baik mencari orang yang sudah paham teknologi tersebut daripada yang belum tahu sama sekali. Kalau pada akhirnya menentukan untuk menggunakan teknologi yang tidak umum, nantinya akan lebih sulit pada proses *hiring*. Kasus nyatanya di Indonesia adalah programmer PHP jauh lebih banyak daripada programmer Python. Kalau memilih teknologi Python, pastinya lebih sulit mencari programmer Python daripada PHP.

Salah satu solusinya mungkin mencari anggota tim yang non-lokal dengan sistem kerja remote, tapi banyak yang lebih memilih tetap menggunakan anggota lokal karena kehadiran anggota tersebut dianggap penting. Beberapa perusahaan yang saya tahu akhirnya membuka kantor cabang *engineering* di kota lain untuk mengisi kebutuhan tersebut.

## Performa?

**Sampai menggangu *user experience*, saya tidak terlalu memperhitungkan performa dari sebuah teknologi**. Tentunya akan lebih sulit jika ingin mencapai *response time* dari Python/Ruby di bawah 100ms dibandingkan menggunakan Java/Go, tetapi mengembangkan aplikasi dengan teknologi Java relatif membutuhkan sumber daya(waktu atau energi) lebih besar daripada Python/Ruby. Dan kenyataannya, ada banyak metode yang dapat dilakukan agar aplikasi Python/Ruby bisa dibawah 100ms(atau bahkan lebih cepat lagi) seperti *caching* :smirk:.

Lagipula, *response time* 100ms bukanlah standar wajib yang perlu diraih aplikasi, itu hanya untuk perbandingan saja. Toh, perfoma aplikasi bukan prioritas di awal-awal pengembangan aplikasi. Nanti akan saya bahas di satu post khusus terkait performa.

## Kesimpulan

Keputusan pemilihan teknologi memang sangat subjektif, tetapi dampaknya akan sangat terasa di masa yang akan datang. Kalau memilih teknologi baru, akan butuh waktu lebih lama dalam pengembangan dan akan ada tantangan dalam ekspansi tim. Kalau memilih teknologi seperti Python/Ruby yang sangat *high level*, masalah performa akan lebih cepat muncul. Semua pilihan ada konsekuensi yang akan dihadapi. Yang terpenting adalah, tahu konsekuensi dari pilihan dan mempersiapkan diri dalam menghadapinya.
