# 📘 Modul 2: Pengenalan Library NumPy

> **Mata Kuliah:** Dasar Kecerdasan Artifisial  
> **Topik:** Komputasi Array dengan NumPy  
> **Level:** Pemula → Menengah

---

## 📋 Daftar Isi

```
1. Tujuan Praktikum
2. Referensi
3. Apa Itu NumPy?
4. Cara Import NumPy
5. Array Biasa vs NumPy Array
6. Atribut Array NumPy
   - 6.1 ndim
   - 6.2 shape
   - 6.3 size
   - 6.4 dtype
7. Deklarasi Array dengan NumPy
8. Penambahan Elemen Array
9. Penghapusan Elemen Array
10. Pengurutan Elemen Array
11. Indexing dan Slicing
12. Penyalinan (Copy) Array
13. Operasi Dasar Array
14. Transpose dan Reshape
15. Soal Latihan Pemrograman
```

---

## 🎯 1. Tujuan Praktikum

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. ✅ Memahami cara mengelola dan memproses komputasi array dengan library NumPy.
2. ✅ Mengetahui fitur-fitur utama yang tersedia di library NumPy.

---

## 🔗 2. Referensi

- 🌐 [Dokumentasi Resmi NumPy v2.0](https://numpy.org/doc/2.0/)

---

## 🧠 3. Apa Itu NumPy?

**NumPy** (*Numerical Python*) adalah library fundamental dalam bahasa pemrograman Python yang digunakan untuk melakukan **komputasi numerik dengan efisiensi tinggi**.

### Keunggulan NumPy:
| Fitur | Manfaat |
|-------|---------|
| 📊 Array Multidimensi | Pengolahan data lebih cepat & efisien dibanding list Python |
| ⚡ Operasi Vektorisasi | Eksekusi operasi matematika tanpa loop eksplisit |
| 🔢 Fungsi Matematika Lengkap | Aljabar linear, statistik, Fourier transform, dll |
| 🧩 Integrasi AI/ML | Dasar untuk pandas, scikit-learn, TensorFlow, PyTorch |
| 💾 Efisiensi Memori | Alokasi memori tetap dengan tipe data homogen |

---

## 📦 4. Cara Import NumPy

```python
# Import standar dengan alias 'np'
import numpy as np
```

> 💡 **Tips:** Selalu eksekusi baris import di awal sesi/script Python Anda.

---

## 🔀 5. Array Biasa vs NumPy Array

| Aspek | Array Biasa (List) | NumPy Array |
|-------|-------------------|-------------|
| **Deklarasi** | `x = [1, 2, 3]` | `x = np.array([1, 2, 3])` |
| **Tipe Data** | Heterogen (campuran) | Homogen (sama semua) |
| **Dimensi** | 1D (nested list untuk multi-D) | Native support 1D, 2D, 3D, ... |
| **Operasi Matematika** | `[1,2,3] + [4,5,6]` → `[1,2,3,4,5,6]` | `np.array([1,2,3]) + np.array([4,5,6])` → `[5,7,9]` |
| **Penggunaan Memori** | Kurang efisien | Lebih efisien |
| **Fungsionalitas** | Dasar | Matematika, aljabar linear, statistik |
| **Slicing** | Dasar: `x[0:2]` | Lanjutan: `x[:, 1:3]` untuk multi-dimensi |
| **Broadcasting** | ❌ Tidak support | ✅ Support operasi array beda ukuran |
| **Penambahan Elemen** | Mudah: `append()` / `+` | Perlu `np.append()` atau array baru |

---

## 📐 6. Atribut Array NumPy

Atribut bawaan untuk mengakses informasi struktur array.

### 6.1 `ndim` — Jumlah Dimensi

```python
import numpy as np

# Array 1D
x = np.array([85, 90, 78, 92, 88])
print("Dimensi array x:", x.ndim)  # Output: 1

# Array 2D
y = np.array([[30, 32, 31], 
              [29, 33, 30], 
              [28, 34, 29]])
print("Dimensi array y:", y.ndim)  # Output: 2
```

#### 📊 Struktur Dimensi Array

| Dimensi | Contoh Struktur | Deskripsi |
|---------|----------------|-----------|
| **1D** | `[1, 2, 3]` | Vektor, satu baris elemen |
| **2D** | `[[1,2,3], [4,5,6]]` | Matriks, baris × kolom |
| **3D** | `[[[1,2],[3,4]], [[5,6],[7,8]]]` | Kubus, depth × baris × kolom |
| **4D** | `[[[[1],[2]],...]]` | Data kompleks (contoh: batch gambar di deep learning) |

---

### 6.2 `shape` — Ukuran Tiap Dimensi

```python
x = np.array([[1, 2, 3], 
              [4, 5, 6]])
print("Shape x:", x.shape)  # Output: (2, 3) → 2 baris, 3 kolom
```

```python
# Perbandingan shape
x = np.array([[1, 2, 3], [4, 5, 6]])           # Shape: (2, 3)
y = np.array([[[7,8,9],[10,11,12]], 
              [[13,14,15],[16,17,18]]])        # Shape: (2, 2, 3)

if x.shape == y.shape:
    print("Shape sama")
else:
    print("Shape berbeda")  # Output: Shape berbeda
```

---

### 6.3 `size` — Total Elemen

```python
x = np.array([[1, 2, 3], [4, 5, 6]])
print("Size x:", x.size)  # Output: 6

# Perbandingan ukuran
a = np.array([1, 2, 3, 4, 5, 6])      # 6 elemen
b = np.array([[5, 6], [7, 8], [9, 10]])  # 6 elemen
print(a.size == b.size)  # Output: True
```

---

### 6.4 `dtype` — Tipe Data Elemen

```python
# Integer
x = np.array([1, 2, 3])
print("Tipe data x:", x.dtype)  # Output: int64

# Float
y = np.array([1.1, 2.2, 3.3])
print("Tipe data y:", y.dtype)  # Output: float64

# String dengan dtype eksplisit
z = np.array(["apple", "banana"], dtype=np.str_)
print("Tipe data z:", z.dtype)  # Output: <U6
```

---

## 🛠️ 7. Deklarasi Array dengan NumPy

### Fungsi Inisialisasi Populer

| Fungsi | Deskripsi | Contoh | Output |
|--------|-----------|--------|--------|
| `np.zeros(shape)` | Array berisi nol | `np.zeros((2,3))` | `[[0. 0. 0.] [0. 0. 0.]]` |
| `np.ones(shape)` | Array berisi satu | `np.ones((3,4))` | `[[1. 1. 1. 1.] ...]` |
| `np.empty(shape)` | Array tanpa inisialisasi (cepat) | `np.empty((2,2))` | `[[... acak ...]]` |
| `np.arange(start, stop, step)` | Rentang dengan interval | `np.arange(0,10,2)` | `[0 2 4 6 8]` |
| `np.linspace(start, stop, num)` | Nilai merata dalam rentang | `np.linspace(0,1,5)` | `[0. 0.25 0.5 0.75 1.]` |
| `np.full(shape, value)` | Array dengan nilai konstan | `np.full((2,2), 7)` | `[[7 7] [7 7]]` |
| `np.random.random(shape)` | Nilai acak [0,1) uniform | `np.random.random((2,3))` | `[[0.12 0.45 ...]]` |
| `np.random.randint(low, high, size)` | Integer acak dalam rentang | `np.random.randint(0,10,size=(3,4))` | `[[2 5 ...]]` |
| `np.fromfunction(func, shape)` | Array dari fungsi indeks | `np.fromfunction(lambda i,j: i+j, (3,3), dtype=int)` | `[[0 1 2] [1 2 3] [2 3 4]]` |

---

## ➕ 8. Penambahan Elemen Array

> ⚠️ Array NumPy memiliki ukuran tetap. Penambahan elemen membuat array **baru**.

### `np.append()`
```python
# 1D
a = np.array([1, 2, 3])
a = np.append(a, [4, 5])
print(a)  # [1 2 3 4 5]

# 2D (tambah baris)
x = np.array([[1, 2], [3, 4]])
x = np.append(x, [[5, 6]], axis=0)
print(x)
# [[1 2]
#  [3 4]
#  [5 6]]
```

### `np.concatenate()`
```python
a = np.array([1, 2])
b = np.array([3, 4])
c = np.concatenate((a, b))
print(c)  # [1 2 3 4]
```

### `np.insert()`
```python
a = np.array([1, 2, 3])
a = np.insert(a, 1, 4)  # Insert '4' di index 1
print(a)  # [1 4 2 3]
```

### `np.stack()` — Menumpuk array di dimensi baru
```python
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
c = np.stack((a, b))
print(c)
# [[1 2 3]
#  [4 5 6]]
print("Shape:", c.shape)  # (2, 3)
```

---

## ➖ 9. Penghapusan Elemen Array

### `np.delete()` — Hapus berdasarkan indeks
```python
# 1D: hapus elemen index 2
x = np.array([1, 2, 3, 4, 5])
x = np.delete(x, 2)
print(x)  # [1 2 4 5]

# 2D: hapus baris (axis=0)
x = np.array([[1,2,3], [4,5,6], [7,8,9]])
x = np.delete(x, 1, axis=0)
print(x)
# [[1 2 3]
#  [7 8 9]]

# 2D: hapus kolom (axis=1)
x = np.delete(x, 1, axis=1)
print(x)
# [[1 3]
#  [7 9]]
```

### `np.where()` + Boolean Masking — Hapus berdasarkan kondisi
```python
x = np.array([1, 2, 3, 4, 5])
# Ganti elemen > 3 dengan NaN, lalu hapus NaN
x = np.where(x > 3, np.nan, x)
x = x[~np.isnan(x)]
print(x)  # [1. 2. 3.]
```

---

## 🔢 10. Pengurutan Elemen Array

| Fungsi | Deskripsi | In-place? |
|--------|-----------|-----------|
| `np.sort(array)` | Mengembalikan array terurut baru | ❌ |
| `array.sort()` | Mengurutkan array asli | ✅ |
| `np.argsort(array)` | Mengembalikan indeks pengurutan | ❌ |

```python
# np.sort()
x = np.array([3, 1, 2])
y = np.sort(x)
print(y)  # [1 2 3]

# array.sort() — in-place
x = np.array([3, 1, 2])
x.sort()
print(x)  # [1 2 3]

# Multi-dimensi: axis=0 (kolom), axis=1/default (baris)
x = np.array([[3,1,2], [9,7,8]])
print(np.sort(x, axis=0))  # Urut per kolom
print(np.sort(x))          # Urut per baris → [[1 2 3] [7 8 9]]
```

---

## 🔍 11. Indexing dan Slicing

### Indexing Sederhana
```python
x = np.array([10, 20, 30, 40, 50])
print(x[2])  # 30
```

### Slicing `[start:stop:step]`
```python
x = np.array([10, 20, 30, 40, 50])
subset = x[1:4]  # indeks 1,2,3
print(subset)  # [20 30 40]
```

### Boolean Indexing
```python
x = np.array([10, 20, 30, 40, 50])
mask = x > 25
print(x[mask])  # [30 40 50]
```

### Fancy Indexing
```python
x = np.array([10, 20, 30, 40, 50])
indeks = [1, 3]
print(x[indeks])  # [20 40]
```

### Multi-Dimensional Indexing
```python
x = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(x[1, 2])  # 6 → baris 1, kolom 2
```

### Ellipsis `...` — Shortcut untuk "semua dimensi tersisa"
```python
x = np.array([[1,2,3], [4,5,6], [7,8,9]])
print(x[1, ...])  # [4 5 6] → sama dengan x[1, :]
```

### `np.ix_()` — Indexing silang baris & kolom
```python
x = np.array([[1,2,3], [4,5,6], [7,8,9]])
rows = [0, 2]
cols = [1, 2]
subset = x[np.ix_(rows, cols)]
print(subset)
# [[2 3]
#  [8 9]]
```

---

## 📋 12. Penyalinan (Copy) Array

| Tipe | Metode | Berbagi Data? | Perubahan Mempengaruhi Asli? |
|------|--------|---------------|------------------------------|
| **Shallow Copy** | `view()`, slicing | ✅ Ya | ✅ Ya |
| **Deep Copy** | `copy()` | ❌ Tidak | ❌ Tidak |

### Shallow Copy — `view()`
```python
x = np.array([1, 2, 3, 4, 5])
y = x.view()
y[0] = 99
print(x)  # [99 2 3 4 5] ← terpengaruh!
```

### Deep Copy — `copy()`
```python
x = np.array([1, 2, 3, 4, 5])
y = x.copy()
y[0] = 99
print(x)  # [1 2 3 4 5] ← tetap asli!
```

> 💡 **Best Practice:** Gunakan `.copy()` jika Anda ingin memodifikasi salinan tanpa mengubah data sumber.

---

## 🧮 13. Operasi Dasar Array

```python
x = np.array([1, 5, 3, 8, 2])

print("Maksimum:", np.max(x))    # 8
print("Minimum:", np.min(x))     # 1
print("Jumlah:", np.sum(x))      # 19
print("Rata-rata:", np.mean(x))  # 3.8

# Operasi dengan axis pada array 2D
x2d = np.array([[1, 2, 3], 
                [4, 5, 6]])
print("Sum per kolom:", np.sum(x2d, axis=0))  # [5 7 9]
print("Sum per baris:", np.sum(x2d, axis=1))  # [6 15]
```

---

## 🔄 14. Transpose dan Reshape

### Transpose — Menukar dimensi
```python
x = np.array([[1, 2, 3], 
              [4, 5, 6]])

# 3 cara transpose:
y1 = x.transpose()
y2 = np.transpose(x)
y3 = x.T

print(y1)
# [[1 4]
#  [2 5]
#  [3 6]]
```

### Reshape — Ubah bentuk tanpa ubah data
```python
x = np.array([1, 2, 3, 4, 5, 6])

# Cara 1: method .reshape()
y = x.reshape((2, 3))

# Cara 2: fungsi np.reshape()
z = np.reshape(x, (2, 3))

print(y)
# [[1 2 3]
#  [4 5 6]]

# 💡 Tips: Gunakan -1 untuk otomatis hitung satu dimensi
w = x.reshape(3, -1)  # → (3, 2)
```

> ⚠️ **Syarat Reshape:** Jumlah elemen harus sama. `6 elemen` → bisa jadi `(2,3)`, `(3,2)`, `(6,1)`, tapi **tidak bisa** `(2,4)`.

---

## ✍️ 15. Soal Latihan Pemrograman

### 🎓 Latihan 1: Sistem Data Mahasiswa
Buat program Python dengan NumPy yang dapat:
- [ ] Menyimpan data mahasiswa: `Nama (str)`, `NIM (str)`, `Nilai (float)`, `TahunMasuk (int)`
- [ ] Menerima input data secara interaktif dari keyboard
- [ ] Menampilkan seluruh data yang telah diinput
- [ ] Menampilkan **nilai tertinggi**, **terendah**, dan **rata-rata**
- [ ] Melakukan pencarian mahasiswa berdasarkan **NIM** atau **Nama**
- [ ] Menampilkan data lengkap hasil pencarian

> 💡 **Hint:** Gunakan array of records (`dtype` terstruktur) atau gabungkan NumPy dengan list/dict untuk field string.

---

### 📦 Latihan 2: Sistem Inventaris Gudang
Buat program Python dengan NumPy yang dapat:
- [ ] Menyimpan data barang: `NamaBarang (str)`, `KodeBarang (str)`, `Jumlah (int)`, `HargaPerUnit (float)`
- [ ] Menerima input data barang secara interaktif
- [ ] Menampilkan seluruh data inventaris
- [ ] Menghitung & menampilkan **total nilai inventaris** (`Jumlah × HargaPerUnit`)
- [ ] Melakukan pencarian barang berdasarkan **KodeBarang** atau **NamaBarang**
- [ ] Menampilkan data lengkap hasil pencarian

> 💡 **Hint:** Pertimbangkan penggunaan `np.recarray` atau pisahkan array numerik (untuk kalkulasi) dan list (untuk metadata string).

---

## 📝 Catatan Penting

```markdown
✅ Selalu import numpy sebagai np di awal script
✅ Gunakan dtype yang sesuai untuk efisiensi memori
✅ Hindari loop untuk operasi numerik — manfaatkan vektorisasi NumPy
✅ Gunakan .copy() jika ingin salinan independen
✅ Manfaatkan broadcasting untuk operasi array beda ukuran
✅ Dokumentasi resmi: https://numpy.org/doc/2.0/
```

---

## 🚀 Next Steps

Setelah menguasai modul ini, lanjutkan ke:
1. 📊 **Modul 3**: Manipulasi Data dengan Pandas
2. 📈 **Modul 4**: Visualisasi Data dengan Matplotlib
3. 🤖 **Modul 5**: Implementasi Machine Learning Dasar

---

> 📌 **Disclaimer**: Materi ini disusun untuk keperluan pembelajaran. Selalu uji kode di environment Anda dan konsultasikan dengan dokumentasi resmi untuk update terbaru.

---

*✨ Selamat belajar dan happy coding dengan NumPy! 🐍🔢*
