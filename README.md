# Aplikasi Pengujian Affix Aksara Jawa (Sriwedari vs KBJ)

> Aplikasi web untuk menguji dan membandingkan hasil transliterasi Ater-ater dan Panambang Aksara Jawa berdasarkan dua paugeran: **Sriwedari** dan **KBJ (Kongres Bahasa Jawa)**.

### Preview
Aplikasi menampilkan dua tabel perbandingan:
- **Hasil menurut Paugeran Sriwedari**
- **Hasil menurut Paugeran KBJ**
- Kolom Latin (Ater-ater + Dasar + Panambang) dan Aksara Jawa

---

## 🎯 Tujuan

1.  Menguji kombinasi affix pada berbagai tipe kata dasar (vokal terbuka vs konsonan)
2.  Menemukan kasus yang memicu `WARNING` di masing-masing paugeran
4.  Membandingkan dua tata tulis Aksara Jawa 

## ✨ Fitur Utama

- **Preset Kata Dasar Lengkap:** 20 kata vokal terbuka (`waca`, `lunga`, `gawé`, dll) dan 50+ kata konsonan (`kukur`, `tulis`, `bakar`, dll)
- **Generator Kombinasi Otomatis:** 
    - 1. Ater-ater + Kata Dasar
    - 2. Kata Dasar + Panambang
    - 3. Kombinasi Lengkap (Ater-ater + Kata Dasar + Panambang)
- **Perbandingan Real-time:** Hasil Sriwedari dan KBJ dirender bersamaan
- **Deteksi Warning Paugeran:** Menampilkan badge kuning jika kombinasi melanggar aturan paugeran
- **Kontrol Tipografi:**
    - Slider ukuran font Aksara Jawa 
    - Slider line-height / spasi vertikal
- **Responsive:** Grid 2 kolom di desktop, 1 kolom di mobile (< 900px)

## 🧩 Daftar Affix yang Diuji

Aplikasi ini menguji kombinasi dari:

**Ater-ater (Awalan):**
```
["N", "dak", "tak", "kok", "ko", "di", "ka", "ke", "sa", 
 "pa", "pi", "kuma", "kami", "kapi", "tar", "pra", "uma", "in", "pating_paN"]
```
**Panambang (Akhiran):**
```
["i", "ake", "aken", "an", "en", "ana", "e", "ipun", "na", "a", "an_e"]
```

## 🔍 Perbedaan Sriwedari vs KBJ (yang terlihat di app ini)

| Aspek | Sriwedari | KBJ |
| :--- | :--- | :--- |
| `tak` & `kok` | Bukan ater-ater baku | Diuji sebagai ater-ater |
| Aturan panambang `an_e`, `ipun` | Lebih konservatif | Lebih fleksibel |
| Warning | `⚠ WARNING PAUGERAN SRIWEDARI:` | `⚠️ WARNING PAUGERAN KBJ:` |

## 📜 Lisensi & Kredit

- **Aplikasi Tester:** Dibuat untuk keperluan pengujian akademis / pelestarian Aksara Jawa.

---

Dibuat dengan semangat nguri-uri Aksara Jawa. ꦧꦸꦢꦪꦗꦮ
