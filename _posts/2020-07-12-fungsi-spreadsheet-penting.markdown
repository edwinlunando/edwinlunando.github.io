---
layout: post
title:  "Fungsi Penting di Spreadsheet"
date:   2020-07-06 11:57:08
author: Edwin Lunando
author_t: edwinlunando
permalink: fungsi-penting-spreadsheet/
---

Beberapa bulan terakhir ini, saya lagi banyak kerjaan yang menggunakan spreadsheet, tepatnya Google Sheet. Layaknya keahlian-keahlian yang lain, di awal-awal saya menggunakan kakas spreadsheet ini, lambat sekali pengerjaannya. Contohnya, saya perlu membuat kolom baru saat mengagregasi data dan banyak perlu copy-paste manual saat bekerja dengan banyak dokumen spreadsheet.

Yah, sederhananya, saya belum ahli dalam menggunakan spreadsheet. Dari dulu cuma tahu fungsi-fungsi dasar seperti SUM, AVERAGE, IF dan VLOOKUP. Padahal, kapabilitas spreadsheet jauh lebih luas dari itu dititik ada yang bilang kalau aplikasi yang lain itu [sebenernya bisa direduksi atau disimplifikasi jadi spreadsheet][1].

Karena [keahlian dalam menggunakan kakas itu penting untuk meningkatkan produktivitas seseorang][2], saya menyisihkan sebagian waktu luang untuk belajar spreadsheet. Berikut merupakan beberapa metode atau fungsi yang saya rasa penting untuk dipahami. Semoga setelah dari artikel ini, kamu bisa lebih efektif dalam mengelola spreadsheet. Sintaksnya menggunakan Google Sheets. kalau pakai aplikasi spreadsheet lain, sintaknya kemungkinan akan berbeda walaupun fungsinya sama. Semua data yang digunakan di artikel ini dapat di akses di [spreadsheet ini][3].

## ARRAYFORMULA untuk Agregasi Data

Fungsi ini lumayan memudahkan hidup dalam melakukan perhitungan yang memadukan lebih dari satu sel. Biasa kan kalau ada kasus seperti ini.

![image](https://user-images.githubusercontent.com/1451080/87246485-f9d72400-c477-11ea-807b-779730032b9d.png)

Kalau kita ingin jumlah semua dari kuantitas dikali dengan harga dari semua baris, kita perlu bikin satu kolom baru untuk menghitung perkalian kuantitas dan harga seperti ini.

![image](https://user-images.githubusercontent.com/1451080/87246504-11aea800-c478-11ea-8e8d-e2ac5db1042a.png)

Nah, dengan menggunakan ARRAYFORMULA, kita tidak perlu menambah kolom baru untuk menampung kalkulasi sementara tersebut.

```
=ARRAYFORMULA(array_formula)

Contoh:
=ARRAYFORMULA(SUM(A2:A6 * B2:B6))
array_formula ini isinya merupakan sebuah ekspresi yang membuat kita bisa melakukan operasi dengan jumlah sel yang banyak.
```

Dengan menggunakan ARRAYFORMULA, penggunaan sel kita akan jadi lebih efisien. Berikut merupakan sheet [contoh penggunaannya][4].

## INDEX dan MATCH daripada VLOOKUP

Kedua metode tersebut sebenarnya tujuannya sama, yaitu mengambil data dari tabel sesuai dengan referensi yang dibutuhkan. Fungsi yang paling umum digunakan itu VLOOKUP, yang sudah saya pelajari mungkin sejak SMP. Ternyata, setelah akhir-akhir ini, saya mencoba menggunakan INDEX dan MATCH, ternyata memang lebih baik.

```
=INDEX(reference, [row], [column])

Contoh:
=INDEX(A2:A, 5, 1)
Artinya, mengembalikan baris kelima dan kolom pertama dari data A2:A.

=MATCH(search_key, range, [search_type])

Contoh
=MATCH(“Baju”, A2:A, 0)
Artinya, mengembalikan nomor baris dari pencarian “Baju” di data A2:A dengan jenis pencarian eksak harus sama. Lihat di sini untuk pencarian jenis lain.
```

Dengan mengkombinasikan MATCH dan INDEX, kita dapat mereplikasikan fungsi VLOOKUP. Berikut contohnya.

```
=VLOOKUP(E3, Master!$A$2:D, 4, 0)

=INDEX(Master!D:D, MATCH(E3, Master!$A$1:A, 0), 0)
```

Hasil dari kedua ekspresi tersebut sama, tapi kita bisa lihat VLOOKUP lebih pendek dan sederhana daripada INDEX dan MATCH. Memang jadi sedikit lebih kompleks, tapi kelebihan INDEX dan MATCH yang pertama adalah referensi kolom yang dinamis. Kalau kedua ekspresi di atas dibandingkan, VLOOKUP itu selalu melihat kolom nomor 4, sedangkan INDEX melihat kolom D. Kalau di sheet Master tersebut kita menambah kolom baru di antara A dan D, hasil VLOOKUP akan berubah, sedangkan INDEX dan MATCH tidak karena referensinya dinamis, tidak spesifik ke sebuah angka kolom. Ini membuat operasi perubahan struktur tabel bisa lebih aman.

Kedua, VLOOKUP itu memaksa nilai yang kita ambil itu berada di kanan karena referensinya merupakan nomor kolom yang dihitung mulai dari yang paling kiri. Kalau INDEX dan MATCH, karena tidak ada limitasi tersebut, bisa saja MATCH-nya di kolam sebelah kanan, sedangkan kolom yang mau diambil oleh INDEX di sebelah kiri. Bisa dibilang, jadinya lebih fleksibel.

Ketiga, yang terakhir, INDEX dan MATCH lebih efisien dalam pemrosesannya karena bisa kita batasi jumlah baris atau kolom yang digunakan dengan mudah. Masalah yang mungkin terjadi dengan VLOOKUP itu pemrosesannya terpaku sama tabel datanya. Kalau kita butuh data dengan jarak kolom yang jauh, VLOOKUP perlu mengevaluasi satu tabel penuh tersebut. Untuk data yang jumlahnya kecil, harusnya tidak ada perbedaan yang signifikan, tapi kalau data yang besar, akan terasa efisiensinya. Berikut merupakan [contoh perbandingan penggunaan keduanya][5].

## IMPORTRANGE dan QUERY untuk Ekstrak dan Filter Data

Untuk kasus kerjaan saya, saya selalu menemukan kasus di mana saya harus menggunakan data dari dokumen yang lain. Daripada saya copy-paste datanya langsung, saya lebih memilih untuk menggunakan fungsi IMPORTRANGE dengan mereferensikan URL dari dokumennya. Dengan begitu, kalau ada perubahan data di dokumen aslinya, data punya saya juga langsung terbaru.

```
=IMPORTRANGE(spreadsheet_url, range_string)

Contoh:
=IMPORTRANGE(“https://docs.google.com/spreadsheets/d/1lCYOuUnmYbMUp2oNroTXxdIcbnniXb-cz5BWYiTIYgs/edit”, “Master!A:D”)
```

Biasanya, setelah saya impor data, tentunya saya selalu butuh memproses datanya. Paling sering itu saya butuh memfilter datanya sesuai dengan kondisi yang saya butuhkan. Contohnya, saya mau ambil data barang yang jenisnya plastik saja.

```
=QUERY(data, query, [headers])

Contoh:
=QUERY(IMPORTRANGE(“https://docs.google.com/spreadsheets/d/1lCYOuUnmYbMUp2oNroTXxdIcbnniXb-cz5BWYiTIYgs/edit”, “Master!A:D”), “SELECT * WHERE Col4 = ‘plastik’”)
```

Query yang digunakan sintaksnya sangat mirip dengan SQL, ya? Itu yang memudahkan penggunaannya. Kasusnya data di atas itu, kolom keempat isinya jenis barangnya. Kita bisa mereferensikan kolom yang lain dengan format Col[kolom ke sekian]. Jadinya Col1, Col2, Col3, Col4, dan seterusnya. Untuk data yang di spreadsheet yang sama, bisa menggunakan huruf kolomnya seperti A, B, C, dan seterusnya. Tentunya, [banyak sintaks query lain][6] yang dapat digunakan untuk kasus spesifik lainnya juga. Ini [contoh pemakaiannya][7].

Dari pengalaman penggunaan ketiga metode ini, dampaknya akan jauh lebih terasa kalau kita lagi menggunakan jumlah baris dan kolom yang besar. Dengan ketiga metode ini, pengalaman dalam berurusan dengan spreadsheet-ku jadi jauh berubah. Saya merasa bisa memproses data yang lebih kompleks dengan lebih efektif.



[1]: https://twitter.com/gcouprie/status/1280448787350196224
[2]: https://gist.github.com/rondy/af1dee1d28c02e9a225ae55da2674a6f#invest-in-iteration-speed
[3]: https://docs.google.com/spreadsheets/d/1lCYOuUnmYbMUp2oNroTXxdIcbnniXb-cz5BWYiTIYgs/edit#gid=1725463389
[4]: https://docs.google.com/spreadsheets/d/1lCYOuUnmYbMUp2oNroTXxdIcbnniXb-cz5BWYiTIYgs/edit#gid=0
[5]: https://docs.google.com/spreadsheets/d/1lCYOuUnmYbMUp2oNroTXxdIcbnniXb-cz5BWYiTIYgs/edit#gid=233406691
[6]: https://developers.google.com/chart/interactive/docs/querylanguage
[7]: https://docs.google.com/spreadsheets/d/1lCYOuUnmYbMUp2oNroTXxdIcbnniXb-cz5BWYiTIYgs/edit#gid=2036210467
