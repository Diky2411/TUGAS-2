# Tugas 2: Membuat Halaman Profil Instagram dengan Tailwind CSS

Proyek ini adalah implementasi ulang halaman profil Instagram yang responsif, kali ini menggunakan framework CSS **Tailwind CSS**. Tujuannya adalah untuk mempraktikkan pendekatan utility-first dalam membangun antarmuka yang kompleks dan responsif dari awal.

---

## Struktur File

├── index.html # File HTML utama yang berisi seluruh struktur dan styling

└── assets

└── img # Folder untuk menyimpan semua gambar yang digunakan


---

## Desain & Pendekatan

- Desain ini sepenuhnya mengadopsi filosofi **mobile-first**. Layout default dirancang untuk layar kecil, kemudian diadaptasi untuk layar yang lebih besar menggunakan responsive prefixes dari Tailwind (`sm:`, `md:`, `lg:`).
- Hampir semua styling (jarak, warna, ukuran, layout) dicapai menggunakan **utility classes** langsung di dalam HTML, meminimalkan kebutuhan akan file CSS kustom.
- Fitur-fitur Tailwind yang menjadi sorotan dalam proyek ini antara lain:
  - **Flexbox & Grid**: Digunakan secara ekstensif untuk layout utama dan galeri foto.
  - **Responsive Prefixes**: `md:flex-row`, `sm:order-1`, `grid-cols-3` adalah contoh bagaimana layout beradaptasi di berbagai ukuran layar.
  - **Utility-First Styling**: Kelas seperti `rounded-full`, `shadow-md`, `font-semibold`, dan `hover:bg-blue-600` digunakan untuk styling mendetail tanpa meninggalkan HTML.
  - **Group Hover**: Efek overlay pada gambar feed diimplementasikan secara elegan menggunakan `group` dan `group-hover:opacity-100`.

---

## Dependensi

Proyek ini menggunakan dependensi eksternal yang dimuat melalui CDN:

- **Tailwind CSS v3**: Script utama yang memungkinkan penggunaan semua utility classes.  
- **Bootstrap Icons 1.11.3**: Untuk ikon yang digunakan di halaman.

---

## Jawaban Pertanyaan Reflektif

### 1. Jelaskan keputusan grid-cols/gap di tiap breakpoint — kenapa begitu?

Keputusan untuk grid-cols dan gap pada galeri foto dibuat berdasarkan pendekatan mobile-first untuk meniru pengalaman pengguna Instagram yang sebenarnya:

- **`grid-cols-3` (Default/Mobile):**  
  Konfigurasi ini dipilih sebagai dasar karena merupakan standar de facto pada antarmuka Instagram. Di layar ponsel yang sempit, menampilkan tiga kolom memberikan keseimbangan terbaik antara ukuran gambar yang dapat dikenali dan jumlah konten yang terlihat, mendorong pengguna untuk scroll.

- **Tidak ada perubahan di breakpoint md atau lg:**  
  Saya sengaja mempertahankan `grid-cols-3` di semua ukuran layar. Alasannya adalah konsistensi visual. Meskipun di desktop ada ruang untuk 4 atau 5 kolom, layout 3 kolom tetap terlihat bersih, premium, dan tidak sesak. Ini adalah pilihan desain yang sadar untuk menjaga estetika minimalis.

- **`gap-1 sm:gap-4` (Responsif Gap):**
  - Di mobile (default), `gap-1` (jarak sangat kecil) digunakan untuk memaksimalkan area yang didedikasikan untuk gambar.  
  - Di layar yang lebih besar (`sm:` dan ke atas), jaraknya ditingkatkan menjadi `sm:gap-4` untuk memberikan "ruang bernapas" antar gambar. Ini membuat galeri terlihat lebih rapi dan tidak melelahkan secara visual saat dilihat di tablet atau desktop.

---

### 2. Bagaimana kamu memanfaatkan utility responsive Tailwind untuk memecahkan masalah layout di mobile?

Utilitas responsif Tailwind adalah kunci untuk menciptakan pengalaman yang mulus dari mobile ke desktop. Berikut beberapa contohnya:

- **Header Profil (`flex-col md:flex-row`):**  
  Di mobile, `flex-col` menumpuk foto profil dan bio secara vertikal, yang merupakan layout paling logis untuk layar sempit. Begitu layar mencapai breakpoint `md`, `md:flex-row` mengubahnya menjadi layout horizontal untuk memanfaatkan lebar layar yang tersedia.

- **Urutan Tombol (`order-2 sm:order-1`):**  
  Di mobile, tombol "Follow/Message" ditempatkan di atas username (`order-1` secara default di `flex-col`) untuk akses cepat. Namun, di layar `sm` ke atas, urutannya dibalik (`sm:order-1` untuk username dan `sm:order-2` untuk tombol) agar sesuai dengan tata letak visual Instagram desktop yang lebih standar.

- **Lebar Tombol (`flex-1 sm:flex-initial`):**  
  Tombol di mobile menggunakan `flex-1` untuk mengisi ruang yang tersedia, membuatnya besar dan mudah ditekan. Di layar `sm`, `sm:flex-initial` membuat ukurannya menyesuaikan kontennya, sehingga tidak meregang secara tidak perlu.

---

### 3. Jelaskan trade-off antara memakai banyak utility classes vs membuat component CSS tersendiri.

Ini adalah perdebatan inti antara filosofi Tailwind dan CSS tradisional. Keduanya memiliki trade-off (plus minus) yang jelas:

#### Menggunakan Banyak Utility Classes (Pendekatan Tailwind)

**Kelebihan:**
- Kecepatan & Tanpa Ganti Konteks: Anda bisa menata gaya langsung di HTML tanpa perlu beralih ke file CSS.  
- Kustomisasi Penuh: Anda tidak dibatasi oleh desain komponen yang sudah ada.  
- Tidak Ada Konflik Nama: Anda tidak perlu pusing memikirkan nama kelas (seperti BEM) atau khawatir tentang specificity.  
- Ukuran File Akhir Kecil: Tailwind akan menghapus semua kelas yang tidak terpakai saat build, menghasilkan CSS yang sangat optimal.  

**Kekurangan:**
- HTML Terlihat "Berantakan": Bagi sebagian orang, daftar kelas yang panjang membuat HTML sulit dibaca.  
- Repetisi: Tanpa framework berbasis komponen (seperti React/Vue), Anda mungkin akan mengulang kombinasi kelas yang sama berulang kali.  

#### Membuat Komponen CSS Tersendiri (misal: `.btn-primary`)

**Kelebihan:**
- HTML "Bersih" & Semantik: Markup terlihat rapi dan lebih mudah dipahami secara struktural (`<button class="btn-primary">`).  
- Reusable & DRY (Don't Repeat Yourself): Anda mendefinisikan gaya sekali di CSS dan bisa menggunakannya di mana saja.  

**Kekurangan:**
- Perlunya Penamaan & Abstraksi: Anda harus memikirkan nama kelas yang baik dan sering kali membuat abstraksi yang sebenarnya tidak diperlukan.  
- CSS Membengkak: File CSS Anda bisa menjadi sangat besar karena berisi gaya yang mungkin tidak pernah Anda gunakan atau lupa untuk dihapus.  
- Risiko Perubahan Global: Mengubah satu properti pada kelas `.btn-primary` akan memengaruhi setiap tombol di situs Anda, yang bisa jadi tidak diinginkan.  

---
