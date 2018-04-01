---
layout: post
title:  "Struktur Data Map"
date:   2018-04-02 11:57:08
author: Edwin Lunando
author_t: edwinlunando
permalink: map/
---

Jadi, kira-kira bulan lalu gua lagi santai belajar bersama seseorang yang baru belajar pemrograman. Dia baru saja masuk jurusan informatika, dan ya, sama seperti orang lainnya yang baru belajar sebuah bidang yang luas dengan kurva pembelajaran yang tinggi, dia banyak sekali bertanya. Gua demen banget sama orang-orang yang keingintahuannya tinggi karena gua pernah ngerasain bingung ndak ada tempat bertanya. Gak enak banget.  Di satu sisi yang lain gua juga paham bahwa oke malu bertanya sesat di jalan, tapi kebanyakan bertanya hilang kemandirian. Jadi, gua selalu mencoba mengarahkan daripada ngejawab langsung pertanyaan demi pertanyaannya.

Tiba-tiba, otak gua terhenti di sebuah pertanyaan

"Kak, ini ada struktur data dictionary ini gimana bikinnya ya?"

Gua terdiam, sedikit bingung karena gua gak bisa jawab langsung. Maksudnya, gua paham cara pakai dictionary, *get-set key-value*, tapi gak tahu cara bikinnya. Selama ini jarang gitu punya inisiatif buat nyari tahu cara kerja modul atau struktur data yang gua pake. Lalu, gua semacam dapat pencerahan, sebenarnya banyak banyak cara kerja modul yang udah gua pake di bahasa level tinggi, tapi gak tahu dalemannya. Jadi, gua membalas pertanyaan dia seakan gua juga ngejawab keingintahuan diri gua sendiri juga.

"Belum tahu, cara kerjanya sih paham, yok cari tahu bareng-bareng"

Akhirnya, yah, ini hasilnya.

## Associative Array

Nama lain dari map. Belum ketemu padanannya yang enak. Tapi gua cukup puas kok dengan map, karena mendeskripsikan sesuai kegunaannya yaitu pemetaan, yang berupa koleksi dari kunci dan nilai. Ini contohnya dengan mengasosiakan nama orang dengan berat badan mereka.

{% highlight bash %}
Key : Value
Luna: 80
Jini: 90
Raka: 65
{% endhighlight %}

Kalau gua mau jawab pertanyaan "Berapa berat Jini?", gua bisa jawab itu dengan kompleksitas konstan(O(1)) atau logaritmik(O(log(n))) sesuai dengan implementasi map yang dibuat. Kita akan bahas itu nanti, tapi poinnya adalah, gua bisa menjawab pertanyaan itu dengan efisien. Tidak perlu menggunakan algoritma pencarian yang kemungkinan kompleksitasnya lebih tinggi. Begini contohnya dalam bahasa Python

{% highlight python %}

berat_badan = {
  'Luna': 80,
  'Jini': 90,
  'Raka': 65,
}

# Jawab pertanyaan "Berapa berat Jini?"
print(berat_badan['Jini'])

{% endhighlight %}

Coba bandingkan dengan penggunaan struktur data dasar seperti array 2 dimensi.

{% highlight python %}

berat_badan = [
  ['Luna', '80'],
  ['Jini', '90'],
  ['Raka', '65'],
]

# Jawab pertanyaan "Berapa berat Jini?"
# Kudu pakai algoritma pencarian

{% endhighlight %}

Itu guna utama map. Operasi-operasi lain seperti pemasukkan(*insertion*) atau penghapusan(*deletion*) juga bisa rata-rata kompleksitasnya konstan atau logaritmik.

## Cara Kerja

Nah, sampai saatnya di bagian yang penting, dalemannya, implementasinya. Ada dua metode yang sangat umum, maksudnya umum itu digunakan oleh bahasa pemrograman sekarang, yaitu dengan *hash table* atau *binary search tree*. Kita bahas dulu dengan menggunakan *hash table*.

### Hash Table

*Hash table* itu sebenarnya hanya *array* biasa saja, hanya penempatan posisi nilainya itu tergantung fungsi *hash* dari kuncinya.

<img src="/images/hash_table.png" alt="hash table data structure" style="width: 100%;"/>

Karena posisinya sudah ditentukan dengan fungsi hash, kita sudah tidak perlu mikir lagi taruh di posisi array sebelah mana. Pokoknya kita tahunya kunci dan nilainya.

{% highlight python %}

class Map:

  def __init__(self):
    self.data = [None] * 30

  def set(self, key, value):
    self.data[hash(key) % len(self.data)] = value

  def get(self, key):
    return self.data[hash(key)]

{% endhighlight %}

Kita bisa menggunakan fungsi hash apapun yang dapat memastikan tiap kunci itu unik, tapi karena keterbatasan ukuran array, sangat mungkin terjadi tabrakan(*collision*). Maksudnya tabrakan itu, dua kunci atau lebih mendapat posisi yang sama. Okelah fungsi hash sudah unik, tapi karena kita menggunakan modulo untuk menyesuaikan ukuran array, bisa saja dua kunci yang jauh berbeda mendapat posisi yang sama.

Contohnya misal kunci `nando` nilainya 12 dengan `naci` nilainya 42 yang ditaruh di array yang ukurannya 30. Artinya dengan modulo 30, kunci `nando` dapat posisi 12(12 % 30) dan `naci` juga dapat posisi 12(42 % 30). Perlu ada metode untuk meresolusi tabrakan ini. Ada banyak sekali metode resolusi tabrakan ini, kita coba bahas 2 yang cukup umum, yaitu *separate chaining* dan *open addressing*. Kedua istilahnya agak *fancy*, yha? Tapi intinya itu, *seperate chaining* itu kalau terjadi tabrakan, nilainya ditampung di posisi yang sama dengan struktur data lain seperti, list. Kalau *open addressing* itu kalau terjadi tabrakan itu dicarikan posisi lain yang masih kosong, entah dengan posisinya dinaikin secara linear, dikali, dipangkat, atau dimasukin fungsi hash lain.

Nah, mari kita revisi *map* di atas dengan metode *open addressing* yang linear.

{% highlight python %}

class Entry:

  def __init__(self, key, value):
    self.key = key
    self.value = value

class Map:

  def __init__(self):
    self.data = [None] * 30

  def set(self, key, value):
    position = get_position(key)

    self.data[position] = Entry(key, value)

  def get(self, key):
    position = get_position(key)

    return self.data[position].value if self.data[position] else None

  def get_position(self, key):
    # mencari posisi yang kosong atau kuncinya sama
    position = hash(key) % len(self.data)

    while self.data[position] != None and self.data[position].key != key:
      position += 1
      if position == len(self.data):
        position = 0

    return position

{% endhighlight %}

Cukup banyak berubah ya? Butuh sebuah struktur data baru karena kita perlu membandingkan kunci. Jadi, butuh informasi terkait kunci dari nilainya. Ku juga menambahkan sebuah fungsi baru `get_position` untuk mencari posisi yang kosong atau mempunyai kunci yang sama untuk kedua kasus `get` dan `set`. Untuk yang `set`, kita nyari yang kosong untuk menaruh nilai baru dan yang sama untuk meperbarui nilai. Kasus yang `get`, kalau dapet kosong artinya memang tidak ada nilai dengan kunci tersebut dan kalau ada yang sama, langsung kembalikan nilainya. Lumayan yha, masih ada satu keresean lagi.

Masih terkait batasan ukuran *array*, kalau dari implementasi di atas, jumlah kunci dan nilai yang dapat ditampung adalah 30. Gimana kalau kita butuh lebih itu? Salah satu solusinya adalah buat panjang map jadi salah satu parameter di inisialisasi dengan jumlah *default* yang besar. Yang kedua, secara dinamis kalau jumlah kunci dibandingkan dengan panjangnya(*load factor*) sudah besar, otomatis memperbesar *array*. Berikut evolusi kodenya.

{% highlight python %}

class Entry:

  def __init__(self, key, value):
    self.key = key
    self.value = value

class Map:

  LOAD_FACTOR_THRESHOLD = 0.7

  def __init__(self):
    self.data = [None] * 30
    self.entry_counter = 0

  def set(self, key, value):

    if float(self.entry_counter) / len(self.data) > self.LOAD_FACTOR_THRESHOLD:
      # bikin baru yang lebih besar
      new_data = [None] * (len(self.data) ** 2)
      # dapetin semua entry
      entries = list(filter(lambda entry: entry is not None, self.data))
      for entry in entries:
        position = self.get_position(entry.key, new_data)
        new_data[position] = entry
      self.data = new_data

    position = self.get_position(key, self.data)
    if self.data[position] == None:
      self.entry_counter += 1

    self.data[position] = Entry(key, value)

  def get(self, key):
    position = self.get_position(key, self.data)

    return self.data[position].value if self.data[position] else None

  def get_position(self, key, data):
    # mencari posisi yang kosong atau kuncinya sama
    position = hash(key) % len(data)

    while data[position] != None and data[position].key != key:
      position += 1
      if position == len(self.data):
        position = 0

    return position
{% endhighlight %}

Yey, akhirnya satu struktur data map selesai diimplementasi. Tentu saja masih banyak yang bisa dikembangkan seperti operasi hapus kunci, optimasi cara ngambil semua entry, dan mencoba metode resolusi tabrakan yang lain. Minimal banget, ini sudah diimplementasikan dengan pertimbangan-pertimbangan yang digunakan di bahasa pemrograman masa kini. Nah, ini perbandingan implementasi di bahasa-bahasa lain.

### Python

- Menggunakan *hash table*
- Kalau load factor di atas 2/3, langsung besarin dikuarat
- Menggunakan [*open addressing* dengan penambahan kuadratik][5]
- Panjang array awal 8

### Java

Di Java, banyak variasi [implementasi map berdasarkan metode-metode yang di atas][6].

- `HashMap`, menggunakan *separate chaining*, dengan linked list sebagai penampung tabrakan. Tapi, [sejak Java 8, diganti menjadi balanced tree][2] biar komplesitas kalau terjadi tabrakan menjadi O(log(n)).
- `TreeMap`, implementasinya datanya menggunakan tree, jadi, kuncinya bisa terurut.

### Ruby

- Menggunakan fungsi hash [Murmur][3]
- List biasa untuk penampung tabrakan. Dengan maksimal panjang list 5. Kalau ada list yang lebih panjang dari itu, ukurannya akan diperbesar dan semua kuncinya dimasukkan ulang.
- [Sampai dengan ukuran 6, semua entri dimasukkan ke satu lokasi][4]

[0]:    https://stackoverflow.com/questions/8997894/what-hash-algorithm-does-pythons-dictionary-mapping-use
[1]:    https://en.wikipedia.org/wiki/Hash_table#Collision_resolution
[2]:    https://stackoverflow.com/questions/43911369/hashmap-java-8-implementation
[3]:    https://en.wikipedia.org/wiki/MurmurHash
[4]:    https://github.com/ruby/ruby/pull/84
[5]:    https://www.laurentluce.com/posts/python-dictionary-implementation/
[6]:    http://tutorials.jenkov.com/java-collections/map.html
