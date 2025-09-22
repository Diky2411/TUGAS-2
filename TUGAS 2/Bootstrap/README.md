# Tugas 1: Membuat Halaman Profil Instagram dengan Bootstrap 5

Proyek ini adalah implementasi halaman profil Instagram yang responsif menggunakan framework CSS Bootstrap 5. Tujuannya adalah untuk mempraktikkan penggunaan sistem grid Bootstrap, termasuk fitur-fitur lanjutannya.

---

## Struktur File
├── index.html # File HTML utama yang berisi seluruh struktur halaman

└── assets

├── css

│   └── style.css # File CSS kustom untuk styling tambahan

└── img # Folder untuk menyimpan gambar


---

## Cara Menjalankan (Build/Run)
Tidak ada proses build yang diperlukan. Cukup buka file `index.html` di browser web modern apa pun (seperti Chrome, Firefox, atau Safari) untuk melihat hasilnya.

---

## Dependensi
Proyek ini menggunakan dependensi eksternal yang dimuat melalui CDN:  
- **Bootstrap 5.3.3 CSS**: Untuk styling dan komponen UI.  
- **Bootstrap 5.3.3 JS Bundle**: Untuk fungsionalitas komponen interaktif Bootstrap.  
- **Bootstrap Icons 1.11.3**: Untuk ikon yang digunakan di halaman.  

---

## Jawaban Pertanyaan

### 1. Mengapa memilih konfigurasi col-tertentu untuk tiap breakpoint?
Konfigurasi kolom `col-4 col-md-4 col-lg-3` dipilih dengan tujuan untuk mengoptimalkan pengalaman pengguna (UX) dan memaksimalkan pemanfaatan ruang layar pada setiap perangkat:

- **Mobile (col-4):** Di layar kecil (breakpoint xs), kelas col-4 menghasilkan 3 kolom. Pilihan ini memberikan keseimbangan yang baik antara ukuran gambar yang masih cukup jelas terlihat dengan jumlah foto yang bisa ditampilkan di layar tanpa perlu scrolling berlebihan. Ini adalah pola yang umum digunakan pada galeri gambar di perangkat mobile.  
- **Tablet (col-md-4):** Pada breakpoint md (tablet), konfigurasi dipertahankan pada 3 kolom. Meskipun layar lebih lebar, menambah kolom menjadi 4 akan membuat setiap gambar menjadi terlalu kecil dan sesak. Dengan tetap di 3 kolom, gambar mendapatkan ukuran yang lebih ideal dan nyaman dipandang.  
- **Desktop (col-lg-3):** Pada layar besar (breakpoint lg ke atas), ruang horizontal sangat melimpah. Kelas col-lg-3 mengubah layout menjadi 4 kolom. Ini memungkinkan pengguna melihat lebih banyak konten secara sekilas, yang merupakan ekspektasi umum saat menjelajah di desktop.  

---

### 2. Bagaimana kamu memastikan tombol Follow/Edit Profile tetap mudah dijangkau di mobile? Jelaskan pendekatannya.
Pendekatan yang digunakan adalah dengan memanfaatkan sifat *mobile-first* dari Bootstrap.  

- **Stacking Otomatis:** Di dalam kode, tombol "Follow" dan "Message" berada di dalam div yang terpisah dari div username. Karena tidak ada kelas col-* spesifik untuk mobile, kedua div ini secara otomatis akan "menumpuk" (stack) secara vertikal di layar kecil.  
- **Urutan Alami HTML:** Sesuai urutan di file HTML, div username muncul lebih dulu, diikuti oleh div tombol. Hasilnya, tombol akan berada tepat di bawah username.  
- **Lebar Penuh & Jarak:** Kelas `w-100` (width 100%) diterapkan pada tombol untuk mobile, membuatnya membentang selebar layar. Ini menjadikan area target sentuh menjadi sangat besar dan mudah dijangkau oleh ibu jari. Kelas `mt-2` (margin-top) juga memberikan jarak visual yang cukup dari elemen di atasnya.  

Kombinasi ini memastikan tombol tidak hanya terlihat jelas, tetapi juga sangat fungsional dan mudah digunakan di perangkat mobile.  

---

### 3. Jika postingan bertambah jadi 50, apa potensi masalah dan bagaimana solusi gridmu mengatasinya?
Jika postingan bertambah menjadi 50, potensi masalah utamanya adalah pengelolaan kode HTML yang tidak efisien (file menjadi sangat panjang dan repetitif) serta potensi layout yang berantakan jika tidak ditangani dengan benar.  

Solusi grid yang ada saat ini mengatasi masalah layout secara efektif:  
- **Wrapping Otomatis:** Seluruh 50 postingan akan tetap berada di dalam satu `<div class="row">`. Sistem grid Bootstrap secara otomatis akan "mematahkan" baris (wrapping) setiap kali total 12 unit kolom terpenuhi. Misalnya, di desktop (col-lg-3), setelah 4 gambar, gambar ke-5 akan otomatis pindah ke baris baru. Ini memastikan grid tetap rapi dan konsisten tanpa perlu membuat elemen `<div class="row">` baru secara manual.  
- **Spasi Konsisten:** Kelas `g-3` (gap) pada div row utama akan menjamin jarak antar gambar tetap seragam, tidak peduli berapa pun jumlah postingannya.  

Namun, untuk masalah pengelolaan kode, solusi grid saja tidak cukup. Dalam skenario nyata, hard-coding 50 elemen adalah praktik yang buruk. Solusi yang lebih baik adalah:  
- **Render Dinamis:** Menggunakan JavaScript untuk mengambil data (misalnya dari sebuah array atau API) dan secara dinamis membuat elemen HTML untuk setiap postingan dalam sebuah perulangan (loop). Ini membuat file `index.html` tetap bersih dan ringkas.  
