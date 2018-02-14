---
layout: post
title:  "Pembagian Tim Dota"
date:   2017-12-18 11:57:08
categories: hobi
author: Edwin Lunando
author_t: edwinlunando
permalink: pembagian-tim-dota/
---

Setelah musim turnamen DotA yang pertama jadi peserta, sekarang ku bantu-bantu jadi panitia untuk musim kedua. Dasarnya? Penasaran aja tentunya, karena ini bukan turnamen DotA profesional, bahkan skalanya lebih kecil dari amatir, cuma lokal satu kantor yang berpartisipasi. Fokusnya serunya, bukan menangnya. Jadi, masalahnya, pembagian timnya sebisa mungkin, kemampuannya rata. Gak ada yang lebih bikin males daripada nonton atau main di pertandingannya yang berat sebelah. Turnamen lalu, baru belasan menit aja udah ada yang *beyond godlike*.

Untungnya, di dunia DotA, ada sistem penilaian kemampuan yang hasilnya angka, matchmaking rating, biasa disebut MMR aja. Kemampuan kan sulit untuk dikuantifikasi, jadi, kami berpegang pada MMR, diharapkan dengan rata-rata MMR setiap tim sama atau mirip, permainannya bisa mendekati imbang. Walaupun [ada beberapa gim olahraga yang mengkuantifikasi kemampuan][0], *resource* kami belum sanggup untuk sampai ke sana.

Oke, jadi ini data MMR 50 pemain yang ikut serta turnamen

{% highlight python %}
[2998, 2705, 3807, 2995, 4062,
  3459, 2186, 3122, 3534, 2501,
  2109, 2676, 2570, 3649, 3390,
  2799, 3556, 3015, 3392, 2288,
  3040, 3619, 4373, 2469, 1934,
  3353, 3065, 3580, 2050, 3460,
  3320, 2255, 2806, 4083, 3155,
  3119, 1812, 3542, 2079, 3147,
  3280, 2887, 4087, 4119, 4914,
  3029, 3786, 4970, 2795, 3779]
{% endhighlight %}

Sengaja ku langsung kasih dalam bentar *array* agar mudah diproses. Terurut dari yang paling besar, ke yang paling kecil. Dari 50 orang ini, akan dibagi ke 10 tim, yang artinya tiap tim berisi 5 orang. Harapannya, tiap tim punya rata-rata MMR yang sangat dekat.

Kalau diperhatikan, masalahnya itu mirip dengan [masalah bin packing][1]. Di masalah tersebut, ada sejumlah barang dengan volume yang berbeda-beda, yang harus dimasukkan ke kotak tertentu yang harapannya meminimalkan jumlah pengunaan kotaknya. Kalau di masalah tersebut variabel kontrolnya ada 2 yaitu volume kotak dan jumlah kotak. Di kasus pembagian tim dota ini, jumlah kotak(tim)nya tetap, tapi volume(jumlah maksimal MMR)nya bisa berubah. Nah, pinginnya kan rata-rata MMR antar tim dekat, jadi jumlah maksimal MMR-nya harus ditekan.

Ada dua pendekatan yang dilakukan *greedy* dan *random*.

## Greedy

Apa ya padanan enak buat algoritma *greedy*? Algoritme tamak? Oke, yang lebih penting untuk diketahui, masalah *bin packing* ini NP(non-polinomial) hard. Yang artinya tidak ada solusi optimal seefisien waktu polinomial. Tapi, karena kita kasus ini tidak perlu mencapai solusi yang **paling** optimal, pakai *greedy* yang solusinya kemungkinan besar tidak optimal pun rapopo.

{% highlight python %}
import random

players = [4970,4914,4373,4119,4087,
  4083,4062,3807,3786,3779,
  3649,3619,3580,3556,3542,
  3534,3460,3459,3392,3390,
  3353,3320,3280,3155,3147,
  3122,3119,3065,3040,3029,
  3015,2998,2995,2887,2806,
  2799,2795,2705,2676,2570,
  2501,2469,2288,2255,2186,
  2109,2079,2050,1934,1812]

random.shuffle(players)

print(players)

mean = reduce(lambda x, y: x + y, players) / len(players)
threshold = mean * 5 * 1.1 # 10 % threshold

teams = {k: [] for k in range(10)}
number_of_team = 10
team_counter = 9
maximum_players = 5

for player in players:
  for counter in range(number_of_team):
    team_counter = 0 if team_counter + 1 >= number_of_team else team_counter + 1
    total_mmr = sum(teams[team_counter])
    if total_mmr + player < threshold and len(teams[team_counter]) <= maximum_players:
      teams[team_counter].append(player)
      break
  print(player, team_counter)

print(teams)

# contoh hasil keluaran
{0: [3040, 2995, 2795, 3534, 3122], 1: [1812, 3320, 3459, 2806, 3119], 2: [3280, 3392, 2998, 2570, 2109], 3: [3065, 3580, 3029, 4083, 3556], 4: [2705, 2255, 3786, 2079, 4970], 5: [4914, 4062, 2676, 2501, 2799], 6: [3353, 3542, 2288, 3649, 1934], 7: [2469, 3147, 4087, 3779, 3015], 8: [2050, 3390, 2887, 3460, 4119], 9: [3155, 3619, 3807, 4373, 2186]}

{% endhighlight %}

Dengan memodifikasi sedikit algoritme *greedy*-nya, ku membagi rata pemain ke semua tim satu per satu terlebih dahulu. Dengan harapan mengurangi penumpukan orang dengan MMR yang serupa dalam satu tim(kasus kalau MMR berurutan).


## Brute Force

Saat ragu mau ngapain, coba *brute force* terlebih dahulu. Sesuai dengan pepatah lama, kami akan mencoba menggunakan kemampuan prosesor untuk mengacak (hampir) semua kemungkinan pasangan tim. Setelah diacak, kita akan memilih yang perbedaan MMR-nya paling kecil antar timnya.

Terus kami coba hitung jumlah kemungkinannya. Dari 50 pemain, dibagi menjadi 10 tim. Jadi, tiap tim ada 5 orang, artinya, 50 kombinasi. `50C5` itu hasilnya 2118760 kemungkinan tim. Dari semua kemungkinan tim tersebut, kita ambil semua pasangan 10 tim yang semua anggota unik. Kan batasannya tiap orang cuma bisa masuk 1 tim. Masalahnya, setelah skripnya dijalankan, sudah ditinggal hampir 1 jam jalannya belum selesai. Terus kan males nunggu lama tuh ya.

Biar nunggunya gak terlalu lama, akhirnya saya pecah jadi 2 bagian, 20 orang dan 20 orang ditambah dengan 2 tim yang sudah saya pisah dari awal. Perhitungannya, `2 * 20C5` itu 31008, jauh lebih sedikit daripada 2118760 sih. Jauh... Ini masalahnya kalau kompleksitasnya faktorial, nambah input sedikit saja(20 ke 50) waktu komputasinya beda jauh. Berikut skrip lengkapnya. Maap, yang kali ini saya tulis pakai ruby, lagi pengen belajar nulis skrip ruby saat itu.

{% highlight ruby %}
players = [4970,4914,4373,4119,4087,4083,4062,3807,3786,3779,3649,3619,3580,3556,3542,3534,3460,3459,3392,3390,3353,3320,3280,3155,3147,3122,3119,3065,3040,3029,3015,2998,2995,2887,2806,2799,2795,2705,2676,2570,2501,2469,2288,2255,2186,2109,2079,2050,1934,1812];
# jumlah mmr tiap tim
goal_mmr = players.sum / players.size * 5

# untuk mengurangi running time
def split_into_two(list_of_players, treshold = 10)
  half_player_size = list_of_players.size / 2
  half_mmr_sum = list_of_players.sum / 2.0
  loop do
    temp = list_of_players.sample(half_player_size)
    return [temp, list_of_players - temp] if (temp.sum - half_mmr_sum).abs < treshold
  end
end
splitted_players = split_into_two(players)

# ngambil 1 tim tiap bagian untuk mengurangi running time lagi
take_1_team = splitted_players.map do |players|
  loop do
    team = players.sample(5)
    break team if (team.sum - goal_mmr).abs < 5
  end
end

(0...splitted_players.size).each do |idx|
  splitted_players[idx] -= take_1_team[idx]
end

# mulai kombinasi tim
def couple_team(list_of_players, treshold = 10.0)
  team_mmr = list_of_players.sum.to_f / list_of_players.size * 5
  list_of_players.combination(5).select do |team|
    (team.sum - team_mmr).abs <= treshold
  end
end
two_splitted_teams = splitted_players.map { |side| couple_team(side) }

# mulai penggabungan tim, ngefilter hanya milih kombinasi yang semua playernya unik
def combine_team(list_of_teams, n)
  list_of_teams.combination(n).select do |team|
    team.flatten.uniq.count == n * 5
  end
end
groups = two_splitted_teams.map { |side| combine_team(side, splitted_players.first.size / 5) }

# pilih yang perbedaan mmr-nya paling rendah
def most_balance(team_combinations, mmr_threshold)
  team_combinations.sort_by { |team_combination| team_combination.map { |team| (team.sum - mmr_threshold).abs**2 }.sum }.first
end
competing_teams = groups.map { |group| most_balance(group, goal_mmr) } + take_1_team
competing_teams = competing_teams.flatten.each_slice(5).to_a


# jumlah total mmr setiap tim untuk perbandingan
teams_mmr = competing_teams.map(&:sum)

# contoh hasil keluaran
puts competing_teams
[[2998, 4087, 1934, 3779, 3065], [3122, 2570, 4914, 2799, 2469], [3542, 2676, 2255, 3320, 4083], [3040, 3390, 3534, 2795, 3119], [4970, 3029, 3015, 2806, 2050], [4373, 4119, 3280, 2288, 1812], [3807, 3619, 3556, 2705, 2186], [3649, 3580, 3147, 2995, 2501], [2079, 3155, 3460, 3786, 3392], [4062, 2887, 3353, 2109, 3459]]

{% endhighlight %}

Skripnya selesai berjalan selama kira-kira 3 menit, jauh lebih nyaman sih dengan waktu jalan yang hitungan menit. Kalau ada masalah pun jalanin ulang skrip pun gak terlalu mikir panjang. Sebenarnya masih ada beberapa bagian yang bisa dioptimasi biar *running time*-nya lebih cepat, tapi kita memilih cukup dulu untuk sekarang.

Kerennya, jelas, nilai standar deviasi dari hasil algoritma *greedy* dan *brute force* lumayan berbeda. Ya toh [*greedy* kan fokusnya cepat, bukan optimalnya][3]. Berikut hasilnya.

{% highlight python %}
import numpy

# hasil algoritma greedy
teams = [[3040, 2995, 2795, 3534, 3122], [1812, 3320, 3459, 2806, 3119], [3280, 3392, 2998, 2570, 2109], [3065, 3580, 3029, 4083, 3556], [2705, 2255, 3786, 2079, 4970], [4914, 4062, 2676, 2501, 2799], [3353, 3542, 2288, 3649, 1934], [2469, 3147, 4087, 3779, 3015], [2050, 3390, 2887, 3460, 4119], [3155, 3619, 3807, 4373, 2186]]

print(numpy.std(map(lambda team: sum(team), teams))
# hasilnya
1038.215391910561

{% endhighlight %}

berikut dari algoritma brute force.

{% highlight ruby %}
require 'descriptive_statistics'

# hasil algoritma brute force
teams = [[2998, 4087, 1934, 3779, 3065], [3122, 2570, 4914, 2799, 2469], [3542, 2676, 2255, 3320, 4083], [3040, 3390, 3534, 2795, 3119], [4970, 3029, 3015, 2806, 2050], [4373, 4119, 3280, 2288, 1812], [3807, 3619, 3556, 2705, 2186], [3649, 3580, 3147, 2995, 2501], [2079, 3155, 3460, 3786, 3392], [4062, 2887, 3353, 2109, 3459]]

puts teams.standard_deviation

# hasilnya
3.521363372331802

{% endhighlight %}

Lumayan jauh ya standar deviasinya, tentu saja kami milihnya yang lebih kecil dengan harapan permainannya bisa lebih imbang. Tapi, DotA kan faktor lainnya banyak, kita liat nanti pas turnamennya lah yha. Untuk sekarang, kami puas dengan algoritma yang kami pilih dan saatnya nonton pertandingan DotA. Cheers! :tada:

[0]:    https://www.vg247.com/2016/09/27/how-ea-calculates-fifa-17-player-ratings/
[1]:    https://en.wikipedia.org/wiki/Bin_packing_problem
[2]:    https://cs.stackexchange.com/questions/72411/proof-that-bin-packing-is-strongly-np-complete
[3]:    https://brilliant.org/wiki/greedy-algorithm/
