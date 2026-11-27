# Mini-Project-5B-
Program Klasifikasi Kategori Anggaran Perjalanan Wisata

Program Python berbasis terminal untuk mengolah data destinasi wisata Indonesia dari file CSV, menghitung estimasi biaya perjalanan per orang per hari, dan mengklasifikasikan anggaran ke dalam tiga kategori: Hemat, Standar, dan Premium.

Mini project mata kuliah Pemrograman Komputer (Prokom), Laboratorium Sistem Informasi dan Keputusan, Departemen Teknik Industri, Fakultas Teknik, Universitas Andalas, 2026 (Kelompok 5B).

Daftar Isi
Fitur
Dataset
Persyaratan
Struktur Proyek
Cara Menjalankan
Menu Program
Contoh Penggunaan
Aturan Klasifikasi dan Rumus
Fungsi dan Kelas Utama
Pengujian
Batasan
Tim Pengembang
Fitur
Login dengan batas 3 kali percobaan.
Membaca file CSV, membersihkan baris yang rusak, dan memvalidasi setiap data.
Menampilkan daftar destinasi dalam tabel, 20 baris per halaman.
Mencari destinasi berdasarkan nama kota.
Mencari destinasi berdasarkan kategori paket (Hemat, Standar, Premium).
Menghitung estimasi biaya perjalanan dari beberapa destinasi, jumlah hari, dan jumlah orang.
Mengklasifikasikan anggaran perjalanan dan memberi catatan singkat untuk tiap kategori.
Pengujian fungsi otomatis dengan assert.
Dataset

Program memakai dataset Indonesia Tourism Destination dalam format CSV, disimpan sebagai destinasi-wisata-indonesia.csv (437 baris data, di luar header). Sumber dataset: https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination.

Kolom yang dipakai program:

Kolom	Jenis	Keterangan
Place_Id	Angka	Nomor identitas destinasi
Place_Name	Teks	Nama destinasi
Category	Teks	Kategori wisata
City	Teks	Kota lokasi destinasi
Price	Angka	Harga tiket masuk (rupiah)
Rating	Angka	Penilaian destinasi

Cara program memperlakukan data:

Pembersihan baris. Titik koma di akhir baris dan tanda kutip pembungkus dibuang sebelum baris dipecah menjadi kolom.
Baris dilewati. Baris yang kolomnya kurang dari 14 atau yang ID-nya bukan angka diabaikan.
Data tidak valid. Baris dengan kolom kosong (nama, kategori, kota, harga, atau rating) atau harga bukan angka dihitung sebagai tidak valid. Baris ini tetap tampil di tabel, dan harga atau rating yang tidak terbaca ditulis -.
Normalisasi rating. Nilai di atas 5 dibagi 10 (contoh: 46 menjadi 4,6).
Persyaratan
Python 3.6 atau lebih baru (memakai f-string).
Hanya pustaka standar (csv dan os). Tidak perlu instalasi tambahan.
Struktur Proyek
.
├── main.py                           # kode program
├── destinasi-wisata-indonesia.csv    # dataset utama
├── tc_norm_01.csv                    # dataset uji: data normal (opsional)
├── tc_kosong_01_header_only.csv      # dataset uji: hanya header (opsional)
└── README.md
Cara Menjalankan
Letakkan destinasi-wisata-indonesia.csv di folder yang sama dengan program (nama file diatur pada konstanta NAMA_FILE).
Jalankan program dari terminal:
bash
python main.py
Masuk dengan akun bawaan program:
Username	Password
adminnya 5B	131126
Setelah 3 kali salah, program berhenti dengan pesan Terlalu banyak salah input. Program dihentikan.

Jika file CSV tidak ditemukan, program menampilkan File 'destinasi-wisata-indonesia.csv' tidak ditemukan.

Menu Program
Menu	Fungsi	Keterangan
1	Daftar tempat	Menampilkan semua destinasi dalam tabel. Tekan Enter untuk halaman berikutnya, q untuk berhenti.
2	Cari kota	Mencari destinasi dengan nama kota (tidak peka huruf besar-kecil, mis. bandung).
3	Cari paket	Memilih kategori 1 (Hemat), 2 (Standar), atau 3 (Premium) untuk menyaring destinasi.
4	Estimasi perjalanan	Menghitung estimasi biaya dari destinasi yang dipilih.
5	Keluar	Menghentikan program.
Contoh Penggunaan

Menu 4: perjalanan 2 hari untuk 3 orang ke Monumen Nasional (Place ID 1, Rp20.000) dan Dunia Fantasi (Place ID 3, Rp270.000).

Lama perjalanan (hari): 2
Jumlah orang          : 3
Place ID (0 = selesai): 1
+ Monumen Nasional (Rp20.000) ditambahkan.
Place ID (0 = selesai): 3
+ Dunia Fantasi (Rp270.000) ditambahkan.
Place ID (0 = selesai): 0

Hasil yang ditampilkan:

Total tiket per orang (2 tempat): Rp290.000
Makan + transport per orang per hari : Rp100.000
Estimasi biaya per orang per hari    : Rp245.000
Estimasi total 2 hari (3 orang)     : Rp1.470.000
KATEGORI ANGGARAN PERJALANAN         : STANDAR
Catatan: anggaran seimbang antara kenyamanan dan biaya.

Pesan yang mungkin muncul saat memilih destinasi: Place ID harus berupa angka., Place ID tidak ditemukan., Tempat ini sudah dipilih., dan Harga tempat ini kosong, tidak bisa dihitung. Bila belum ada destinasi yang dipilih, perhitungan dibatalkan.

Aturan Klasifikasi dan Rumus
Komponen biaya tetap (konstanta di kode)
Konstanta	Nilai	Arti
BIAYA_MAKAN	Rp60.000	Biaya makan per orang per hari
BIAYA_TRANSPORT	Rp40.000	Biaya transportasi per orang per hari
BATAS_HEMAT	Rp200.000	Batas atas kategori Hemat
BATAS_STANDAR	Rp400.000	Batas atas kategori Standar
BARIS_PER_HALAMAN	20	Jumlah baris tabel per halaman
Rumus estimasi (Menu 4)
total_tiket     = jumlah harga tiket semua destinasi yang dipilih (per orang)
total_semua     = (total_tiket + (BIAYA_MAKAN + BIAYA_TRANSPORT) x hari) x orang
per_orang_hari  = round(total_semua / orang / hari)

Harga tiket dihitung sekali per orang, sedangkan biaya makan dan transport dihitung per hari.

Kategori anggaran perjalanan (berdasarkan per_orang_hari)
Kategori	Kondisi
Hemat	kurang dari atau sama dengan Rp200.000
Standar	di atas Rp200.000 sampai Rp400.000
Premium	di atas Rp400.000
Kategori paket (kolom "Kategori Paket" pada tabel, Menu 1 sampai 3)

Kategori ini menilai harga tiket satu destinasi dan dihitung dari data: harga valid diurutkan, lalu dibagi menjadi tiga bagian sama besar.

batas_paket_1 = harga_urut[n // 3]
batas_paket_2 = harga_urut[(2 * n) // 3]

Harga kurang dari atau sama dengan batas_paket_1 masuk Hemat, kurang dari atau sama dengan batas_paket_2 masuk Standar, selebihnya Premium. Untuk dataset 437 data, batasnya Rp2.000 dan Rp10.000. Jika data valid kurang dari 3, program memakai batas Rp200.000 dan Rp400.000. Destinasi tanpa harga yang valid diberi label Tidak Valid.

Fungsi dan Kelas Utama
Nama	Kegunaan
format_rupiah(angka)	Mengubah angka menjadi format rupiah, mis. Rp1.500.000
klasifikasi_anggaran(biaya)	Menentukan Hemat, Standar, atau Premium dari biaya per orang per hari
minta_angka(pesan)	Meminta bilangan bulat minimal 1 dan mengulang sampai valid
bersihkan_baris(baris)	Membersihkan titik koma dan tanda kutip berlebih pada satu baris CSV
class Tempat	Menyimpan satu destinasi. Metode: harga_angka(), rating_angka(), data_kosong(), kategori_harga_interval(), cetak_baris()
class AplikasiWisata	Mengatur seluruh alur program
AplikasiWisata.login()	Memeriksa username dan password (3 percobaan)
AplikasiWisata.baca_csv()	Membaca, membersihkan, memvalidasi data, dan menghitung batas kategori paket
AplikasiWisata.cari_tempat(teks)	Mencari destinasi berdasarkan Place ID
AplikasiWisata.tampilkan_tabel(daftar, judul)	Menampilkan tabel dengan pembagian halaman
AplikasiWisata.menu_daftar_semua()	Menu 1
AplikasiWisata.menu_cari_kota()	Menu 2
AplikasiWisata.menu_cari_kategori_paket()	Menu 3
AplikasiWisata.menu_estimasi_perjalanan()	Menu 4
AplikasiWisata.jalankan_tes()	Pengujian fungsi dengan assert
AplikasiWisata.jalankan()	Memeriksa file data lalu menjalankan program
Pengujian

Pengujian fungsi. jalankan_tes() berisi 10 pernyataan assert untuk format_rupiah, klasifikasi_anggaran (nilai batas 200.000, 200.001, dan 400.001), serta metode kelas Tempat. Bila semuanya benar, tampil Semua pengujian fungsi LULUS.

Test case (rincian lengkap di laporan, Bab III):

Skenario	Dataset	Hasil yang diharapkan	Status
Data normal dan lengkap	tc_norm_01.csv (3 data: Rp20.000, gratis, Rp270.000)	3 data valid, 0 tidak valid. Estimasi 2 hari untuk 1 orang dengan tiket Rp20.000 = Rp110.000 per orang per hari, kategori Hemat	PASS
Data kosong	tc_kosong_01_header_only.csv (hanya header)	Program tidak error dan menampilkan File CSV terbaca tetapi tidak ada data yang valid.	PASS

Tracing. Laporan memuat 10 langkah penelusuran, dari inisialisasi konstanta, login, pembacaan 437 data, perhitungan batas kategori paket, sampai estimasi biaya dan keluar dari menu.

Batasan
Dataset yang dipakai adalah destinasi-wisata-indonesia.csv dengan kolom nama, kategori, kota, harga tiket, dan rating.
Biaya makan dan transport adalah nilai tetap yang ditentukan di dalam kode, bukan data dari dataset.
Program tidak membahas pemesanan tiket, transportasi, penginapan, maupun pembayaran.
Username dan password login tertulis langsung di kode (akun demo), bukan sistem akun sungguhan.
Tim Pengembang

Kelompok 5B

Raisa Athira Rendra
Syifa Aulia Rasca
Puti Nurul Atillah
Mhd. Aidil Oktoberi

Asisten Pembimbing: Suroso Aditya Wibowo

Dosen Pengampu: Dr. Eng. Ardhian Agung Yulianto

Laboratorium Sistem Informasi dan Keputusan, Departemen Teknik Industri, Fakultas Teknik, Universitas Andalas, 2026.
