---
layout: post
title:  "5 Tahap Kesedihan Versi Programmer"
date:   2016-01-26
categories: hidup insinyur
author: Edwin Lunando
author_t: edwinlunando
permalink: 5-tahap-kesedihan
header_image: /images/sedih.png
---

Manusia selalu berusaha memahami dirinya sendiri. Bahkan, ada orang yang merumuskan tahapan-tahapan yang akan kita lewati kalau kita bersedih. Teori tersebut disebut dengan [5 tahap kesedihan][1]. Beberapa hari yang lalu, saya secara sadar melewati 5 tahap tersebut, tapi dengan permasalahan di dunia pemrograman. Langsung saja ke ceritanya.

## Awalnya

Pada hari senin yang cerah, saya memulai pagi dengan memasak sarapan seperti layaknya hari-hari lain. Saat makan, saya dihubungi rekan kerja sekantor saya.

"Win, kok API *backend search recipe* berubah?" (*paraphrasing*, karena yang original jauh lebih kasar)

Saat itu pula saya langsung panik(walaupun kesalahannya di fase testing). Saya tidak merasa pernah mengubah [API][2] yang sudah sesuai dengan kontrak di awal. Mulailah 5 tahap kesedihan tersebut.

##  Denial

"Gak mungkin berubah. Kecuali ada orang lain yang ubah."

Kata-kata tersebut muncul terus berulang-ulang di kepala saya. Toh, saya ingat dengan yakin tidak melakukan perubahan yang dimaksud. Saya langsung membuka laptop saya dan mulai menginvestigasi masalah ini.

Saya coba jalankan di laptop saya, ternyata memang benar API-nya ada yang salah. Ya tapi tetap saja, saya gak ngerasa mengubah.

Setelah kira-kira 30 menit mencari, saya teringat kembali. Oh iya, saya memang tidak pernah mengubah API, tapi saya memperbarui pustaka API *open source* yang saya gunakan. Saya coba kembalikan ke versi awal, API saya berjalan normal kembali. :confused:

## Anger

"Ngaco banget sih pustaka ini"

"Yang bikin gimana sih?"

Pada saat itu, saya marah ke yang bikin pustaka ini karena dokumentasinya (mungkin) salah. Saya sudah menggunakan sesuai petunjuk yang dia buat, tetapi tidak jalan. Kalau yang bikin pustaka bikin cara penggunaannya salah ya gimana ya. **Di tahap ini saya masih gak tahu siapa yang salah**. Masih mungkin saja saya yang penggunaannya salah.

Setelah itu, saya mulai membuat laporan kepada sang pemilik pustaka. Berharap akan dibalas dengan cepat. Saya tidak memutuskan untuk menggunakan versi yang lama karena ada beberapa fitur baru yang saya gunakan di versi baru. Kalau saya kembalikan ke versi lama, makan waktu lagi. :angry:

## Bargaining

"Kalau aja pake pustaka yang lain"

1 jam berlalu lagi(yang sebenernya sebentar banget), belum ada jawaban sama sekali dari sang pengelola pustaka. Waktu berjalan sangat lama pada saat fase ini. Mood saya semakin turun dan turun.

Saya mulai berpikir kalau pakai pustaka yang lain yang biasa saya pakai, pasti gak bakal ketemu masalah ini. Padahal kenyataannya, kalau pake pustaka lain juga pasti ketemu masalah. Cuma ya masalahnya beda aja. :dizzy_face:

## Depression

"..."

Kan katanya **desperate times call for desperate measures**. Saya gak mikir apa-apa di tahap ini. Saya coba semua cara yang saya tahu untuk mendapatkan jawaban. Saya akhirnya menanyakan permasalahan saya ke beberapa forum pemrograman(contohnya [stackoverflow][3]), padahal saya tahu saya gak bakal jawabannya(karena masalahnya sangat spesifik). Ini cuma usaha putus asa dari saya saja.

Sebenarnya ya saya bisa saja coba ubah kode pustakanya sendiri, tapi saya kira bakal lebih repot dan memilih mencari solusi yang lebih baik. Di fase ini, saya membuka semua halaman web yang terkait dengan pustaka tersebut berhadap dapat pencerahan. Kenyataannya, tidak berhasil.

Saya coba ubah kodenya manual, gagal karena saya belum paham terkait internal dari pustaka tersebut. :weary:

## Acceptance

"ya udah lah"

Di tahap ini, saya sudah ngerasa baik kembali. Sudah terima aja lah, *deal with it*. Saya sudah tidak merasa bermasalah kalau akhirnya turun ke versi yang lama. Saya coba jalan-jalan sebentar di tahap ini untuk sekadar istirahat saja. Kira-kira 1/2 jam lah fase ini. :relieved:

## Akhirnya

Akhirnya, dengan sisa-sisa tenaga dan mood yang sudah rendah, saya membaca kode dari pustaka tersebut satu per satu, baris demi baris. Dari sana, saya pahami arsitektur dalam pustakanya dari awal hingga akhir. **Setelah saya baca dan terus baca, akhirnya saya sangat yakin bahwa dokumen petunjuk yang dia tulis salah**. Kali ini, saya tahu cara pakai yang benar. Selanjutnya, saya perbaiki dan *deploy* API saya dalam waktu kurang dari 5 menit. :grinning:

## Kesimpulan

Ini [trit yang saya buat di Github][4] sebagai kenang-kenangan. Setelah itu, **saya memutuskan untuk memperbaiki dokumentasi dari pustaka tersebut**. Huff. Ternyata, tidak sampai 1 jam setelah saya menyelesaikan masalah saya, sang pengelola pustaka membalas dan menjawab masalah saya(yang sebenarnya sudah selesai). Yah memang sebagai programmer yang menggunakan pustaka *open source* ini sudah menjadi risiko. Toh, kalau bertemu dengan masalah yang sejenis, saya tinggal melewati 5 tahap tersebut lagi. :joy:

[1]:    http://grief.com/the-five-stages-of-grief/
[2]:    https://en.wikipedia.org/wiki/Application_programming_interface
[3]:    http://stackoverflow.com/
[4]:    https://github.com/rails-api/active_model_serializers/issues/1466
