---
layout: post
title:  "Pola Desain: Repository"
date:   2017-12-18 11:57:08
categories: pola arsitektur repository
author: Edwin Lunando
author_t: edwinlunando
permalink: repository/
---

Sepanjang tahun 2017 ini, gua ngembangin aplikasi-aplikasi kecil yang fiturnya hanya ada 1 atau 2. Salah satunya itu adalah sebuah bot Telegram yang ngasih info hari ini sudah *deploy* aplikasi apa saja. Jadi, tiap kali ada deployment yang selesai, proses deployment akan menembak API dari bot tersebut. Jadi, gua tinggal ngomong `/releases` ke bot tersebut buat tahu sudah *deploy* apa aja hari ini.

Cukup sederhana bukan? Namun, saat mulai gua kembangin, gua bimbang mau milih basis datanya. Pilihan pertama gua selalu basis data relasional seperti MySQL atau SQLite, tapi temen ngide buat pake redis. Jadi, kami sepakat unyuk nyoba pakai redis dulu, tapi bikin kodenya sedemikian sehingga basis datanya mudah diganti. Di sini lah pola *repository* bekerja.

<figure>
    <img src="/images/repository.png" alt="repository patter" style="width: 100%;"/>
    <figcaption>Pola repository</figcaption>
</figure>

Pola repository sesungguhnya adalah sebuah jembatan antara domain bisnis(*client business logic*) dengan sumber data(*data source*). Pemisahan ini ditujukan untuk abstraksi komunikasi dengan sumber data. Domain bisnis tidak perlu tahu atau ikut campur implementasi pemanggilan ke sumber data karena yang mereka butuhkan adalah hasil balikan sesuai dari sumber data. Dengan begitu, implementasi komunikasi ke sumber data akan terisolasi sehingga kita dapat menggantinya tanpa menganggu logika bisnis aplikasi. Berikut merupakan contoh implementasinya.

Pertama-tama kita membuat sebuah entitas bisnis dan *interface*.

{% highlight ruby %}
class Repository

  attr_accessor :date, :state, :created_at

  def to_json
    {
        date: self.date,
        state: self.state,
        created_at: self.created_at
    }
  end

end

class AbstractRepository

  def save_release(release)
    raise NotImplementedError
  end

  def get_releases
    raise NotImplementedError
  end

end
{% endhighlight %}

Lalu sebuah kelas implementasi dari *interface* tersebut. Implementasinya menggunakan Redis dan MySQL

{% highlight ruby %}

class RedisReleaseRepository < AbstractRepository

  ...
  def save_release(release)
    @client.rpush('releases', release.to_json)
  end

  def get_releases
    @client.get('releases')
  end

end

class MySQLReleaseRepository < AbstractRepository

  ...
  def save_release(release)
    statement = @client.prepare('INSERT INTO releases VALUES (?, ?, ?)')
    statement.execute(release.date, release.state, release.created_at)
  end

  def get_releases
    statement = @client.prepare('SELECT * FROM releases')
    results = statement.execute
  end

end

{% endhighlight %}

Lalu, tinggal digunakan sesuai kebutuhan, deh.

{% highlight ruby %}

class RepositoryService

  def initialize(storage)
    @storage = storage
  end

  def save(release)
    @storage.save_release(release)
    # kode yang lain
  end

  def get
    @storage.get_releases
    # kode yang lain
  end

end

{% endhighlight %}

Tinggal ganti parameter jika ingin menggunakan basis data yang lain pada saat

{% highlight ruby %}
Repository.new(MySQLReleaseRepository.new)
# atau
Repository.new(RedisReleaseRepository.new)
{% endhighlight %}

Untuk basis data lain, cukup dengan mengimplementasi kelas storage sesuai dengan basis datanya lalu gunakan sesuai kebutuhan.

Pola ini tidak hanya dapat digunakan untuk basis data saja. Pengalaman saya, untuk servis-servis *third party* seperti email yang banyak pilihan, kita dapat mengimplementasi pola *repository*, yang sebenarnya cukup mirip dengan pola *adapter*, juga untuk memudahkan penggantian kebutuhan.
