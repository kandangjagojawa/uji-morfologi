# Aplikasi Pengujian Affix Aksara Jawa (Sriwedari vs KBJ)

> Aplikasi web untuk menguji dan membandingkan hasil transliterasi Ater-ater dan Panambang Aksara Jawa berdasarkan dua paugeran: **Sriwedari** dan **KBJ (Kongres Bahasa Jawa)**.

Aplikasi ini membantu peneliti, pengembang font Aksara Jawa, dan pembelajar bahasa Jawa untuk melihat perbedaan rendering ater-ater (awalan) dan panambang (akhiran) secara side-by-side.

### Preview
Aplikasi menampilkan dua tabel perbandingan:
- **Kiri:** Hasil menurut Paugeran Sriwedari
- **Kanan:** Hasil menurut Paugeran KBJ
- Kolom Latin (Ater + Dasar + Panam) dan Aksara Jawa (dengan font Ngayogyakarta)

---

## 🎯 Tujuan

1.  Memvalidasi konsistensi engine transliterasi `sriwedari.js` dan `kbj.js`
2.  Menguji kombinasi affix pada berbagai tipe kata dasar (vokal terbuka vs konsonan)
3.  Menemukan kasus yang memicu `WARNING PAUGERAN` di masing-masing paugeran
4.  Membandingkan visual Aksara Jawa untuk keperluan penyempurnaan font

## ✨ Fitur Utama

- **Preset Kata Dasar Lengkap:** 20 kata vokal terbuka (`waca`, `lunga`, `gawé`, dll) dan 50+ kata konsonan (`kukur`, `tulis`, `bakar`, dll)
- **Generator Kombinasi Otomatis:** 
    - 1. Ater-ater + Kata Dasar
    - 2. Kata Dasar + Panambang
    - 3. Kombinasi Lengkap (Ater-ater + Kata Dasar + Panambang)
- **Perbandingan Real-time:** Hasil Sriwedari dan KBJ dirender bersamaan
- **Deteksi Warning Paugeran:** Menampilkan badge kuning jika kombinasi melanggar aturan paugeran
- **Kontrol Tipografi:**
    - Slider ukuran font Aksara Jawa (1rem - 3rem)
    - Slider line-height / spasi vertikal (1 - 2.5)
- **Sandbox Engine:** Memuat `sriwedari.js` dan `kbj.js` via `new Function()` agar tidak konflik di global scope
- **Responsive:** Grid 2 kolom di desktop, 1 kolom di mobile (< 900px)

## 📁 Struktur Proyek

```
/ (root)
├── index.html          # Aplikasi utama (file ini)
├── sriwedari.js        # Engine transliterasi Paugeran Sriwedari [wajib]
├── kbj.js              # Engine transliterasi Paugeran KBJ [wajib]
├── ngayogyann.ttf      # Font Aksara Jawa Ngayogyakarta
└── README.md
```

> **Catatan:** `sriwedari.js` dan `kbj.js` harus mengekspos fungsi `prosesParamasastra()` dan `transliterasiKalimat()` serta elemen DOM dengan ID: `selAter`, `inDasar`, `selPanam`, `outParamLatin`, `outParamJawa`, `paramWarningArea` (aplikasi ini akan membuatnya otomatis jika belum ada).

## 🧩 Daftar Affix yang Diuji

Aplikasi ini menguji kombinasi dari:

**Ater-ater (Awalan):**
```js
["N", "dak", "tak", "kok", "ko", "di", "ka", "ke", "sa", 
 "pa", "pi", "kuma", "kami", "kapi", "tar", "pra", "uma", "in", "pating_paN"]
```
Khusus Sriwedari: `tak` dan `kok` difilter (tidak diuji).

**Panambang (Akhiran):**
```js
["i", "ake", "aken", "an", "en", "ana", "e", "ipun", "na", "a", "an_e"]
```

## ⚙️ Cara Kerja Teknis

1.  `initAplikasi()` melakukan `fetch()` untuk `sriwedari.js` dan `kbj.js`
2.  Kode dieksekusi dalam sandbox: `new Function(code + 'return {prosesParamasastra, transliterasiKalimat}')()`
3.  Saat user memilih kata dasar, `generateKombinasi()` dipanggil untuk kedua engine:
    - Membuat elemen DOM virtual tersembunyi untuk mensimulasikan input engine asli
    - Loop `aterOnly`, `panamOnly`, dan `combination`
    - Mengambil `outParamLatin.value`, `outParamJawa.innerText`, dan `paramWarningArea.innerText`
4.  `renderTable()` mengelompokkan hasil menjadi 3 seksi dan menghilangkan duplikat

Fungsi `formatLatinForUI()` membersihkan artefak seperti `nnanné` -> `nané` dan tanda hubung ganda.

## 🚀 Cara Menjalankan

Karena aplikasi menggunakan `fetch()` untuk memuat engine, harus dijalankan via server, bukan `file://`.

**Opsi 1: Python (paling mudah)**
```bash
python -m http.server 8000
# buka http://localhost:8000
```

**Opsi 2: VS Code Live Server**
Klik kanan `index.html` -> Open with Live Server

**Opsi 3: GitHub Pages**
Push semua file ke repo dan aktifkan Pages. Aplikasi sudah kompatibel.

## 🎨 Kustomisasi

- **Ganti font:** Edit `@font-face` di `<style>` dan ganti file `ngayogyann.ttf`
- **Tambah preset:** Edit array `kataVokal` dan `kataKonsonan` di dalam `<script>`
- **Tambah affix:** Edit `daftarAterBase` dan `daftarPanamBase`
- **Warna tema:** Edit `:root` CSS variables `--primary-color`, `--accent-color`

## 🔍 Perbedaan Sriwedari vs KBJ (yang terlihat di app ini)

| Aspek | Sriwedari | KBJ |
| :--- | :--- | :--- |
| `tak` & `kok` | Tidak dianggap ater-ater baku (difilter) | Diuji sebagai ater-ater |
| Aturan panambang `an_e`, `ipun` | Lebih konservatif | Lebih fleksibel |
| Warning | `⚠ WARNING PAUGERAN:` | `⚠️ WARNING PAUGERAN KBJ:` |

Aplikasi ini sangat berguna untuk melihat perbedaan tersebut secara visual pada Aksara Jawa.

## 📜 Lisensi & Kredit

- **Font:** Ngayogyakarta - silakan cek lisensi font di sumber aslinya.
- **Engine:** `sriwedari.js` & `kbj.js` adalah hak milik pembuat masing-masing.
- **Aplikasi Tester:** Dibuat untuk keperluan pengujian akademis / pelestarian Aksara Jawa.

---

Dibuat dengan semangat nguri-uri Aksara Jawa. ꦧꦸꦢꦪꦗꦮ
