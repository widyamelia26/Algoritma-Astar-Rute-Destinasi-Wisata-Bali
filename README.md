# Sistem Rekomendasi Rute Terpendek Menuju Destinasi Wisata di Bali
Bali sebagai salah satu kota wisata populer di Indonesia, menerima 9,8 juta kunjungan wisatawan lokal dan 5,3 kunjungan wisatawan mancanegara. Meskipun demikian, wisatawan sering kali menghadapi tantangan dalam merencanakan rute perjalanan mereka karena keterbatasan informasi mengenai berbagai lokasi destinasi wisata serta rute terbaik-nya. Sistem ini diharapkan dapat membantu mengatasi permasalahan tersebut dengan mengidentifikasi rute optimal dari Pelabuhan Gilimanuk dan Bandara I Gusti Ngurah Rai (titik yang seringkali menjadi titik awal bagi wisatawan) ke berbagai destinasi wisata, sehingga memberikan pengalaman perjalanan yang lebih efisien dan menyenangkan.

## Metode A-Star Search
Pada studi kasus ini, algoritma A* (A-star) digunakan untuk mencari jalur terpendek dari Pelabuhan Gilimanuk dan Bandara Ngurah Rai ke berbagai destinasi wisata di Bali. A* adalah salah satu algoritma pencarian jalur terpendek yang paling umum digunakan dalam pemetaan dan navigasi. Algoritma ini menggabungkan fungsi biaya (_cost function_) dan heuristik untuk menemukan jalur yang optimal. oleh karena itu, algoritma A-star dinilai sangat efektif karena tidak hanya mempertimbangkan jarak aktual antara dua titik, tetapi juga memanfaatkan informasi tambahan berupa heuristik. Heuristik yang digunakan dalam studi ini adalah jarak Haversine, yang memperhitungkan kelengkungan bumi dalam penghitungan jarak antar node, sehingga menghasilkan estimasi jarak yang lebih akurat.

## Representasi Ruang Keadaan
Wisatawan akan diminta untuk memasukkan lokasi awal dan lokasi tujuan yang akan dicapai. Kemudian sistem akan memberikan rute tercepat dengan berbagai tambahan lokasi destinasi wisata yang dapat dikunjungi sebelum mencapai lokasi tujuan, setiap lokasi wisata akan direpresentasikan ke dalam node.

## Prasyarat
* Python versi 3.x
* _Libraries_:
  * `heapq`, `math`, `matplotlib`, `networkx`
  * `pandas` untuk membaca file Excel
  * `ipywidgets` untuk interaksi dengan pengguna
  * `IPython.display` untuk menampilkan output
  
## Detail Kode
### _Import Libraries_
- `heapq`: Untuk implementasi antrian prioritas pada algoritma A*.
- `math`: Untuk perhitungan matematika, seperti formula Haversine.
- `matplotlib.pyplot` dan `networkx`: Untuk visualisasi graf.
- `pandas`: Untuk membaca data dari file Excel.
- `IPython.display`, `ipywidgets`, `BytesIO`, `base64`: Untuk interaksi dan visualisasi di notebook.

### Kelas Graph
* `__init__`: Menginisialisasi graph dengan list edge kosong.
* `add_edge`: Menambahkan edge antara dua node dengan jarak.
* `heuristic`: Menghitung fungsi heuristik dari setiap node menuju node tujuan menggunakan rumus Haversine
* `a_star`: Mengimplementasikan algoritma A* untuk menemukan jalur terpendek.
* `reconstruct_path`: Membangun jalur dari node awal ke node tujuan yang telah didapatkan dari `a_star`
* `draw_path`: Menggambar dan menyimpan visualisasi graph dari rute terbaik.
* `get_edge_cost`: Mengambil besaran jarak dari dua node.

### Input Data
Data _langtitude_ dan _longtitude_ dari setiap destinasi wisata akan di-_input_ ke `destinations_df` dan data jarak antar lokasi destinasi wsisata akan di-_input_ ke `edges_df`.
```
file_path = 'tourist_destinations.xlsx'
destinations_df = pd.read_excel(file_path, sheet_name='Sheet1')
edges_df = pd.read_excel(file_path, sheet_name='Edges')
```
### Inisialisasi Objek `Graph`
Menginisialisasi objek `Graph` untuk menyimpan node (destinasi) dan edge (jalur) di antara mereka. Kemudian, mengisi _dictionary_ `pos` dengan koordinat geografis (_longitude_, _latitude_) dari setiap destinasi wisata yang diambil dari `destinations_df`  serta menambahkan koneksi antar destinasi dengan jarak sebagai bobot dari data `edges_df` ke dalam graph menggunakan `add_edge()`.
```
# Membuat graph kosong
g = Graph()
pos = {}
for index, row in destinations_df.iterrows():
    pos[row['Destination']] = (row['Longitude'], row['Latitude'])
for index, row in edges_df.iterrows():
    g.add_edge(row['From'], row['To'], row['Cost'])
```

### Visualisasi Graph
Graph destinasi divisualisasikan menggunakan `networkx` yang menampilkan node sebagai destinasi dan edge sebagai jalur antar destinasi.
```
plt.figure(figsize=(100, 300))
# Menggambar graf dengan posisi node dan label edge
...
plt.show()
```
### Pencarian Jalur Tependek dari Pelabuhan Gilimanuk dan Bandara I Gusti Ngurah Rai
Melakukan pencarian jalur terpendek dari Pelabuhan Gilimanuk dan Bandara I Gusti Ngurah Rai, sebagai lokasi awal, ke berbagai destinasi wisata di bali dengan menggunakan algoritma A-star
```
start_points = ['pelabuhan gilimanuk', 'bandara ngurahrai']

# Inisialisasi list untuk menyimpan hasil
results = []

# Jalankan A* untuk mencari jalur terpendek
for start in start_points:
    for goal in destinations_df['Destination']:
        if goal != start:
            path, total_km = g.a_star(start, goal)
            ...
```
### Widget Interaktif
* _Dropdown Widget_: Memungkinkan pengguna memilih lokasi awal dan lokasi tujuan dari daftar destinasi yang tersedia.
* _Button Widget_: Memicu fungsi A* ketika pengguna menekan tombol "Cari Jalur Terpendek".
* _Output Label_ : Menggunakan widget `Output` untuk menampilkan hasil dari algoritma A*, yaitu jalur terpendek, total jarak, dan visualisasi _graph_.
* _on_button_click_ : Memanggil algoritma A* ketika tombol ditekan dan hasilnya akan ditampilkan di _widget output_.

## Layanan Interaktif Pengguna
Pengguna dapat memilih lokasi awal dan tujuan melalui dropdown yang interaktif. Jalur terpendek akan dihitung ketika tombol ditekan dan hasilnya ditampilkan di _widget output_, baik dalam bentuk teks maupun graf.

### Panduan Penggunaan Kode bagi Pengguna
1. Unduh file Excel tourist_destinations.xlsx tersedia sebagai data input yang dibutuhkan
2. Instal semua _library_ yang diperlukan 
3. Jalankan kode dalam notebook Jupyter atau lingkungan yang mendukung IPython dan widgets.
4. Pilih Lokasi Awal dan Tujuan dengan menggunakan widget dropdown yang tersedia.
5. Klik tombol untuk mencari jalur terpendek.
6. Hasil Jalur Terpendek: Klik tombol Cari Jalur Terpendek untuk melihat hasil rute terbaik beserta visualisasi graf yang menampilkan jalur.


