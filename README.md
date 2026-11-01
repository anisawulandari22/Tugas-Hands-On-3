# Tugas Hands-On 3: Pandas Lanjutan - Employee Attrition

Repositori ini berisi pengerjaan **Tugas Hands-On 3** menggunakan studi kasus **Kasus 05: Employee Attrition (HR Analytics)**. Proyek ini mendemonstrasikan alur kerja ilmu data end-to-end mulai dari audit kualitas data, pembersihan (*cleaning*), analisis lanjutan dengan *groupby*, hingga penyiapan data untuk pemodelan machine learning tanpa kebocoran data (*data leakage*).

---

## 📊 Ringkasan Kasus & Dataset

- **Sektor:** HR Analytics
- **Jenis Tugas:** Klasifikasi Biner (*Employee Attrition* / Prediksi Keluar Perusahaan)
- **Jumlah Baris Awal:** 1.200 baris
- **Variabel Utama:** Demografi karyawan, departemen, tingkat kepuasan kerja, gaji bulanan, lembur, dan status keluar perusahaan.

---

[Buka Notebook di Google Colab](https://colab.research.google.com/drive/1tjfKzUyXUHmVoI8a0n-YoGxaH8wLBnqq?usp=sharing)

## 🔍 Hasil Audit Kualitas Data

Berdasarkan fungsi audit kualitas (`cek_kualitas`), berikut adalah ringkasan perubahan kondisi data sebelum dan sesudah pembersihan:

| Metrik Kualitas | Sebelum Pembersihan | Sesudah Pembersihan |
| :--- | :--- | :--- |
| **n_baris** | 1200 | 1200 |
| **n_duplikat** | 0 | 0 |
| **n_missing** | 574 | 0 |
| **n_outlier** | 0 | 0 |

* **Penanganan Missing Value:** Dilakukan imputasi menggunakan nilai tengah (*median*) untuk kolom numerik kontinu/diskrit dan nilai terbanyak (*modus*) untuk kolom kategorikal.

---

## 💡 Tiga Temuan Utama yang Dapat Ditindaklanjuti

1. **Departemen dengan Risiko Tertinggi (*Sales* & *Finance*):** 
   Departemen Sales memiliki jumlah karyawan dan angka *resign* tertinggi (84 orang), disusul oleh Finance (73 orang). Manajemen HR disarankan untuk meninjau ulang target atau beban operasional di kedua departemen ini.
2. **Korelasi Kepuasan Kerja yang Rendah:** 
   Departemen Sales dan Finance tercatat memiliki skor rata-rata kepuasan kerja terendah ($\approx 2.0$) dibandingkan departemen lainnya ($\approx 3.0$), mengindikasikan bahwa ketidakpuasan kerja merupakan pemicu utama perpindahan karyawan.
3. **Faktor Non-Finansial sebagai Pendorong Utama:** 
   Meskipun rata-rata gaji bulanan di semua departemen relatif setara (berkisar antara Rp32 juta hingga Rp35 juta), faktor kenyamanan kerja dan kepuasan lingkungan lebih dominan dalam membedakan volume keluar masuk pegawai.

---

## ⚙️ Persiapan Pemodelan (Modeling Preparation)

* **Train-Test Split:** Dilakukan pemisahan data dengan parameter `stratify=y` guna menjaga proporsi kelas target yang seimbang.
* **ColumnTransformer:** Menerapkan `StandardScaler` untuk fitur numerik dan `OneHotEncoder` untuk fitur kategorikal. Proses *fit* **hanya dilakukan pada data train** untuk mencegah terjadinya *data leakage*.

---

*Dibuat untuk memenuhi Tugas Hands-On 3 - Artificial Intelligence Course.*
