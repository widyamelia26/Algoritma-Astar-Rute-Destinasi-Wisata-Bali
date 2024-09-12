# Sistem Rekomendasi Rute Terpendek Menuju Destinasi Wisata di Bali
Bali sebagai salah satu kota wisata populer di Indonesia, menerima 9,8 juta kunjungan wisatawan lokal dan 5,3 kunjungan wisatawan mancanegara. Meskipun demikian, , wisatawan sering kali menghadapi tantangan dalam merencanakan rute perjalanan mereka karena keterbatasan informasi mengenai berbagai lokasi destinasi wisata serta rute terbaik-nya. Sistem ini diharapkan dapat membantu mengatasi permasalahan tersebut dengan mengidentifikasi rute optimal dari Pelabuhan Gilimanuk dan Bandara I Gusti Ngurah Rai (titik yang seringkali menjadi titik awal bagi wisatawan) ke berbagai destinasi wisata, sehingga memberikan pengalaman perjalanan yang lebih efisien dan menyenangkan.

# Representasi Ruang Keadaan
Wisatawan akan diminta untuk memasukkan lokasi awal dan lokasi tujuan yang akan dicapai. Kemudian sistem akan memberikan rute tercepat dengan berbagai tambahan lokasi destinasi wisata yang dapat dikunjungi sebelum mencapai lokasi tujuan, setiap lokasi wisata akan direpresentasikan ke dalam node.

# Metode A-Star Search

# Detail Kode
## Fungsi Heuristik
```
def heuristic(self, node, goal):
    # Koordinat lintang dan bujur untuk node dan goal
      lat1, lon1 = pos[node]
      lat2, lon2 = pos[goal]
      
      # Konversi derajat ke radian
      lat1, lon1, lat2, lon2 = map(math.radians, [lat1, lon1, lat2, lon2])
      # Haversine formula
      dlat = lat2 - lat1
      dlon = lon2 - lon1
      a = math.sin(dlat / 2) ** 2 + math.cos(lat1) * math.cos(lat2) * math.sin(dlon / 2) ** 2
      c = 2 * math.atan2(math.sqrt(a), math.sqrt(1 - a))
      # Radius bumi dalam kilometer
      R = 6371.0
      distance = R * c
      return distance
```
Fungsi heuristik ini akan menghitung beban dari setiap node ke lokasi tujuan dengan menggunakan ukuran haversine. 

## Fungsi Pencarian Rute Terbaik dengan A-Star
## Fungsi untuk Membuat Graph

# Tahapan Menjalankan Kode
