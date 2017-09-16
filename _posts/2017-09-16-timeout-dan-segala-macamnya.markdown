---
layout: post
title:  "Timeout dan Segala Macamnya"
date:   2017-09-16
categories: timeout
author: Edwin Lunando
author_t: edwinlunando
permalink: timeout/
---

2 bulan terakhir, gua banyak menangani komunikasi antar aplikasi yang jaraknya jauh. Jauhnya itu, dari [Depok ke Oregon][0] banget. Kalau sebelumnya, gua paling jauh itu paling dari Indonesia ke server Singapura atau Jepang. Beda banget dari sisi latency dan reliability. Ping ke server di jaringan yang sama itu di bawah 4 milidetik, ping ke server Singapura 20 milidetik, sedangkan ping ke server Oregon itu 200 milidetik.

Masalah kedua itu muncul saat *throughput* komunikasinya membesar. Saat sebuah aplikasi dihujani permintaan, responnya bakal melambat. Pengalaman gua sih, yang sering terjadi itu kita dapet kesalahan yang sangat terkenal yaitu `Timeout Error`. Masalahnya sederhana, **klien, yang ngirim permintaan, punya ekspektasi sebuah permintaan itu diselesaikan dalam sejumlah waktu dan server tidak dapat memenuhi permintaan sesuai tenggat yang klien kasih**. Sama lah kayak semua masalah di dunia ini, perbedaan ekspektasi.

Jadi, ini panduan untuk mengoptimasi ekspektasi klien, komputer yang mengirimkan permintaan, terhadap server apa pun bentuk permintaannya.

## Timeout

Berikut beberapa [jenis timeout][1] yang perlu ditangani:

1. *connect* - waktu membuka koneksi
1. *read* - waktu menerima data
1. *write* - waktu mengiriman data

Prinsipnya sederhana, tidak terlalu kecil, dan tidak terlalu besar. Lihat waktu respon di 90-99 persentil dan maksimalnya. Kalau maksimalnya masih sesuai ekspektasi, tentukan waktunya sedikit di atas batas maksimum. Contoh, waktu respons di 90 persentil itu 160 milidetik, maksimalnya 250 milidetik. Gua bakal ambil 500-1000 milidetik sebagai batas timeout-nya.

Jangan mengambil batas waktu timeout terlalu tinggi karena dalam kasus sebuah respon server sedang lambat bermasalah, yang kita inginkan adalah segera memutus koneksi tersebut agak tidak menambah beban dari server tersebut.

Banyak kakas untuk mengukur, [salah satu yang paling sederhana itu `curl`][2]. Yak, standar klien HTTP bisa ngasih detil dari semua waktu yang rentan timeout. Begini, pertama-tama, buat sebuah berkas bernama `curl-format.txt`, lalu isi dengan.

{% highlight bash %}

            time_namelookup:  %{time_namelookup}s\n
               time_connect:  %{time_connect}s\n
            time_appconnect:  %{time_appconnect}s\n
           time_pretransfer:  %{time_pretransfer}s\n
              time_redirect:  %{time_redirect}s\n
         time_starttransfer:  %{time_starttransfer}s\n
                            ----------\n
                 time_total:  %{time_total}s\n

{% endhighlight %}

Lalu, jalankan curl dengan format.

{% highlight bash %}

curl -w "@curl-format.txt" -o /dev/null -s http://www.google.com

{% endhighlight %}

Hasilnya akan seperti ini.

{% highlight bash %}

            time_namelookup:  0.013s
               time_connect:  0.035s
            time_appconnect:  0.000s
           time_pretransfer:  0.035s
              time_redirect:  0.000s
         time_starttransfer:  0.068s
                            ----------
                 time_total:  0.068s

{% endhighlight %}

`time_connect`(waktu untuk membuat koneksi) itu dapat digunakan untuk menentukan waktu timeout *connect* sedangkan, untuk *read* dan *write* biasanya saya menggunakan `time_total` dikurangi dengan `time_connect`.

Setiap klien yang memberikan pekerjaan ke server lain, pasti minimal ada pengaturan waktu timout untuk pembuatan koneksi dan eksekusi kerjanya. Jadi, kita tinggal setel sesuai dengan ekspektasi kita.

## Retry

Nah, karena kita [gak boleh mengasumsikan jaringan itu bakal stabil][3], akan ada kasus di mana server tidak ada masalah, tapi tetap terjadi timeout karena masalah jaringan sementara. Entah permintaan itu terlambat diteruskan ke server, datanya hilang di tengah pengiriman, atau [kabel internet bawah laut digigit hiu][6]. Ada banyak sekali kemungkinannya. Nah, kasus yang kalau-dicoba-lagi-ada-kemungkinan-sukses ini, kita mau ada mekanisme coba kirim permintaan kembali.

Ini berikut contohnya dengan menangkap exception terkait timeout.

{% highlight ruby %}

begin
  retries ||= 0
  # kirim permintaan ke server
rescue Timeout::Error => e
  # coba lagi kalau masalahnya terkait timeout
  retry if (retries += 1) < 4
  raise e
end

{% endhighlight %}

Biasanya kalau ada kesalahan timeout yang tidak dicoba kembali, pengguna yang harus coba ulang. Mekanisme **retry** ini berguna agar mengurangi beban pengguna.

## Keep Alive

Karena [pembuatan koneksi TCP itu mahal][4], untuk kasus *throughput* yang tinggi, disarankan untuk menggunakan [mode `keepalive` dari koneksi TCP][5] untuk menyimpang koneksi untuk permintaan selanjutnya.

Tentunya tetap ada biaya untuk mempertahankan koneksi persisten ini, tapi yang penting itu biayanya jauh lebih rendah daripada membuat koneksi yang baru.

## Tenang

Yak, kira-kira begitulah inti sari dari lelah 2 bulan terakhir ini ngurusin server yang berjauhan ini. Minimal banget, tidur gua bisa jauh lebih tenang setelah implementasi solusi tersebut. Dah, ku istirahat dulu dari serangan `Timeout Error` ini.

[0]: https://www.google.co.id/search?q=depok+to+oregon+distance&oq=depok+to+oregon+distance
[1]: https://github.com/ankane/the-ultimate-guide-to-ruby-timeouts
[2]: https://blog.josephscott.org/2011/10/14/timing-details-with-curl/
[3]: https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing
[4]: https://stackoverflow.com/questions/31378403/how-much-data-it-cost-to-set-up-a-tcp-connection
[5]: http://ltxfaq.custhelp.com/app/answers/detail/a_id/1512/~/tcp-keepalives-explained
[6]: https://www.wired.com/2014/08/shark_cable/
