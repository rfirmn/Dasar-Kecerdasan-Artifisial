# 1. Apa itu Scikit-Fuzzy?

scikit-fuzzy adalah library Python yang kuat untuk mengimplementasikan Fuzzy Logic. Berbeda dengan logika klasik yang kaku (0 atau 1), logika fuzzy menangani "derajat kebenaran". Library ini sangat populer dalam sistem kendali industri, AI game, dan sistem pendukung keputusan.

# 2. Persiapan & Instalasi

Pastikan Anda memiliki Python (versi 3.6+) dan library pendukung seperti NumPy dan Matplotlib untuk visualisasi.

Instalasi via Terminal

```ptyhon
pip install scikit-fuzzy numpy matplotlib
```


# 3. Komponen Inti dalam Scikit-Fuzzy

Ada tiga pilar utama yang harus dipahami:

Antecedent (Input): Variabel yang memengaruhi keputusan (misal: Kelembaban, Suhu).

Consequent (Output): Hasil keputusan (misal: Durasi Siram, Kecepatan Kipas).

Membership Function (MF): Kurva yang menentukan bagaimana setiap titik data dipetakan ke nilai keanggotaan antara 0 dan 1.

# 4. Eksplorasi Fungsi Keanggotaan (Membership Functions)

Scikit-Fuzzy mendukung berbagai bentuk kurva. Pemilihan bentuk ini bergantung pada karakteristik data:

trimf (Triangular): Berbentuk segitiga. Paling sederhana dan efisien secara komputasi.

trapmf (Trapezoidal): Berbentuk trapesium. Bagus jika ada rentang nilai yang memiliki tingkat keanggotaan 1 (penuh) secara stabil.

gaussmf (Gaussian): Berbentuk lonceng. Memberikan transisi yang sangat halus (smooth).

# 5. Implementasi: Sistem Rekomendasi Tips Restoran

Kita akan membangun sistem dengan 2 Input dan 1 Output.

## A. Definisi Variabel & Semesta (Universe)

```python
import numpy as np
import skfuzzy as fuzz
from skfuzzy import control as ctrl

# Input: Kualitas Makanan (0-10) dan Pelayanan (0-10)
makanan = ctrl.Antecedent(np.arange(0, 11, 1), 'makanan')
servis = ctrl.Antecedent(np.arange(0, 11, 1), 'servis')

# Output: Jumlah Tips (0-25%)
tips = ctrl.Consequent(np.arange(0, 26, 1), 'tips')
```


## B. Otomatisasi vs Manual Fungsi Keanggotaan

```python
# Cara Cepat: Otomatis membagi menjadi 3 kategori (poor, average, good)
makanan.automf(3)
servis.automf(3)

# Cara Kustom: Manual menggunakan segitiga (trimf)
tips['rendah'] = fuzz.trimf(tips.universe, [0, 0, 13])
tips['sedang'] = fuzz.trimf(tips.universe, [0, 13, 25])
tips['tinggi'] = fuzz.trimf(tips.universe, [13, 25, 25])
```

## C. Membangun Aturan (Fuzzy Rules)

Aturan menghubungkan input ke output menggunakan logika AND, OR, dan NOT.

```python
rule1 = ctrl.Rule(servis['poor'] | makanan['poor'], tips['rendah'])
rule2 = ctrl.Rule(servis['average'], tips['sedang'])
rule3 = ctrl.Rule(servis['good'] | makanan['good'], tips['tinggi'])
```


# 6. Visualisasi: Melihat Logika di Balik Layar

Salah satu fitur terbaik skfuzzy adalah kemampuannya untuk memvisualisasikan kurva.

```python
# Melihat kurva fungsi keanggotaan
makanan.view()
servis.view()
tips.view()
```

Catatan: Anda memerlukan matplotlib untuk menjalankan perintah .view().

# 7. Proses Defuzzifikasi

Setelah aturan dijalankan, sistem menghasilkan area fuzzy. Defuzzifikasi adalah proses mengubah area tersebut menjadi satu angka pasti (Crisp Value).

skfuzzy mendukung beberapa metode:

Centroid (Default): Mencari titik pusat area.

Bisector: Membagi area menjadi dua bagian sama luas.

MOM (Mean of Maximum): Rata-rata dari nilai dengan keanggotaan tertinggi.

Menjalankan Simulasi:

```python
tipping_sim = ctrl.ControlSystemSimulation(ctrl.ControlSystem([rule1, rule2, rule3]))

# Masukkan Input Nyata
tipping_sim.input['makanan'] = 7.0
tipping_sim.input['servis'] = 9.8

# Hitung
tipping_sim.compute()

print(f"Hasil Defuzzifikasi (Tips): {tipping_sim.output['tips']:.2f}%")
tips.view(sim=tipping_sim) # Visualisasi hasil pada kurva
```


# 8. Ringkasan Alur Kerja

Define: Tentukan rentang nilai (Universe).

Fuzzify: Buat kategori (Membership Functions).

Rule: Hubungkan input-output dengan logika IF-THEN.

Simulate: Masukkan data input.

Defuzzify: Ambil hasil angka pastinya.

# 9. Proyek Latihan

Cobalah modifikasi kode di atas untuk kasus "Sistem Penentu Durasi Cuci Mesin Otomatis":

Input 1: Tingkat Kekotoran Pakaian (0-100).

Input 2: Berat Beban (0-10 kg).

Output: Waktu Cuci (10-60 menit).

Materi ini disusun untuk memperdalam pemahaman logika fuzzy pada ekosistem Python.
