# Sistem Rekomendasi Rute Terpendek Menuju Destinasi Wisata di Bali
Bali sebagai salah satu kota wisata populer di Indonesia, menerima 9,8 juta kunjungan wisatawan lokal dan 5,3 kunjungan wisatawan mancanegara. Meskipun demikian, , wisatawan sering kali menghadapi tantangan dalam merencanakan rute perjalanan mereka karena keterbatasan informasi mengenai berbagai lokasi destinasi wisata serta rute terbaik-nya. Sistem ini diharapkan dapat membantu mengatasi permasalahan tersebut dengan mengidentifikasi rute optimal dari Pelabuhan Gilimanuk dan Bandara I Gusti Ngurah Rai (titik yang seringkali menjadi titik awal bagi wisatawan) ke berbagai destinasi wisata, sehingga memberikan pengalaman perjalanan yang lebih efisien dan menyenangkan.

## Representasi Ruang Keadaan
Wisatawan akan diminta untuk memasukkan lokasi awal dan lokasi tujuan yang akan dicapai. Kemudian sistem akan memberikan rute tercepat dengan berbagai tambahan lokasi destinasi wisata yang dapat dikunjungi sebelum mencapai lokasi tujuan, setiap lokasi wisata akan direpresentasikan ke dalam node.

# Metode A-Star Search

## Requirements
- `matplotlib` untuk visualisasi
- `networkx` untuk operasi graph
- `pandas` untuk manipulasi data
- `ipython` untuk tampilan interaktif
- `openpyxl` untuk membaca file Excel
## Format Data Input 
### Contoh Data Input
## Cara Kerja dari Kode
### Kelas Graph
* `__init__`: Menginisialisasi graph dengan list edge kosong.
* `add_edge`: Menambahkan edge antara dua node dengan jarak.
* `heuristic`: Menghitung fungsi heuristik dari setiap node menuju node tujuan menggunakan rumus Haversine
* `a_star`: Mengimplementasikan algoritma A* untuk menemukan jalur terpendek.
* `reconstruct_path`: Membangun jalur dari node awal ke node tujuan yang telah didapatkan dari `a_star`
* `draw_path`: Menggambar dan menyimpan visualisasi graph dari rute terbaik.
* `get_edge_cost`: Mengambil besaran jarak dari dua node.


