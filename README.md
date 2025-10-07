# EDA-Healthcare-Kelompok-7

- Nadia Clearesta Shafira (103102400007)
- Zerlina Agustiya Putri (103102400009)
- Moch Rafi Nanda Prayogo (103102400002)
- Abdul Khaliq (103102400078)

## 1) Load Data
- pandas: Mengelola dan menganalisis data dalam bentuk tabel (DataFrame).
- numpy: untuk perhitungan numerik.
- matplotlib.pyplot: Membuat visualisasi data seperti grafik.
- Seaborn: Untuk visualisasi data statistik.
- pd.read_csv(path): Membaca file CSV dan menyimpannya ke variabel df.
- df.shape: Menunjukkan ukuran data (jumlah baris, jumlah kolom).
- df.head(): Menampilkan 5 baris pertama dari dataset.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

path = "healthcare_dataset.csv"
df = pd.read_csv(path)
print(df.shape)
df.head()
```

## 2) Basic Information About The Dataset
- df.info(): Memberikan ringkasan kolom, tipe data, dan jumlah data yang tidak kosong.
- df.describe(include='all').T: Menampilkan ringkasan statistik dari seluruh kolom dalam DataFrame df, lalu .T membuat tabelnya ditranspos (diputar) agar lebih mudah dibaca (kolom jadi baris, dan sebaliknya).

```python
df.info()
df.describe(include='all').T
```

# 3) Cek Nilai Duplikat dan Nilai Unik
- df.duplicated().sum(): Menghitung jumlah baris yang sama persis (duplikat).
- df[df.duplicated()]: Menampilkan baris-baris yang terduplikasi.
- df.nunique(): Menunjukkan berapa banyak nilai unik di setiap kolom, berguna untuk melihat keragaman data.

```python
print("Jumlah duplikat:", df.duplicated().sum())
df[df.duplicated()]
df.nunique()
```

## 4) Visualisasi Jumlah Unik
Visualisasi jumlah nilai unik adalah cara untuk menampilkan banyaknya nilai berbeda (unik) yang terdapat pada setiap kolom dalam sebuah dataset.
- df.nunique(): Menghitung jumlah nilai unik.
- plt.figure(figsize=(10, 6)): Mengatur ukuran gambar dengan lebar 10 dan tinggi 6 inci.
- unique_counts.plot(kind='bar', color='black'): Menampilkan data unik dalam bentuk grafik batang (bar chart).
- plt.title: Memberi judul pada grafik.
- plt.xlabel: Memberi label pada sumbu X (horizontal).
- plt.ylabel: Memberi label pada sumbu Y (vertikal).
- plt.show(): Menampilkan grafik di layar.

```python
unique_counts = df.nunique()

plt.figure(figsize=(10, 6))
unique_counts.plot(kind='bar', color='black')

plt.title('Jumlah Nilai Unik per Kolom')
plt.xlabel('Nama Kolom')
plt.ylabel('Jumlah Nilai Unik')

plt.show()
```

## 5) Menemukan Null Values
Null value (nilai kosong) adalah data yang tidak memiliki nilai atau hilang dalam dataset.
- isnull(): Mengecek apakah data tersebut terdapat nilai kosong (null) atau tidak.
- df.isnull().sum(): Menghitung berapa banyak nilai kosong (True) di setiap kolom.

```python
print("Nilai Null:")
df.isnull()

print("Jumlah Nilai Null per Kolom:")
df.isnull().sum()
```

## 6) Replace Semua Null Values


```python
df_filled = df.copy()
for col in df_filled.columns:
    if pd.api.types.is_numeric_dtype(df_filled[col]):
        df_filled[col] = df_filled[col].fillna(df_filled[col].mean())
    else:
        mode_series = df_filled[col].mode(dropna=True)
        if mode_series.empty:
            df_filled[col] = df_filled[col].fillna('unknown')
        else:
            df_filled[col] = df_filled[col].fillna(mode_series.iloc[0])

print("Null setelah penggantian:")
display(df_filled.isnull().sum().to_frame(name="null_after_fill").T)
```

## 7) Mengetahui Tipe Data dari Dataset


```python
from IPython.display import display
display(df_filled.dtypes.to_frame(name="dtype"))
```

## 8) Filter Data
- df: adalah DataFrame utama.
- df['Age'] > 20: Membuat kondisi pertama, yaitu hanya ambil baris dengan umur lebih dari 20.
- df['Blood Type'] == 'B+': kondisi kedua, hanya ambil baris dengan golongan darah B+.

```python
filtered_df = df[(df['Age'] > 20) & (df['Blood Type'] == 'B+')]

print(f"Jumlah data sebelum difilter: {len(df)}")
print(f"Jumlah data setelah difilter: {len(filtered_df)}")
print("Data Hasil Filter: ")
display(filtered_df.head(10))
```

## 9) Create a Box Plot
- select_dtypes():  Memilih kolom tertentu berdasarkan tipe datanya
- (include=['int64', 'float64']): Menyaring kolom yang bertipe angka saja.
- data=filtered_df[numeric_cols]: Hanya menggunakan kolom numerik dari dataset.

```python
plt.figure(figsize=(10,6))
numeric_cols = filtered_df.select_dtypes(include=['int64', 'float64']).columns
sns.boxplot(data=filtered_df[numeric_cols], color='lightcoral')
plt.title('Box Plot')
plt.ylabel('Nilai')
plt.show()
```

## 10) Correlation
- filtered_df[numeric_cols]: Mengambil subset data yang hanya berisi kolom numerik tersebut.
- .corr(): Menghitung matriks korelasi antar kolom numerik.
- plt.figure(figsize=(8,6)): Menentukan ukuran gambar (8 inci x 6 inci).
- corr: Data yang divisualisasikan
- annot=True: Menampilkan nilai korelasi di dalam tiap kotak
- cmap='RdBu': Menentukan warna gradasi merah ke biru (Merah = korelasi negatif, biru = korelasi positif)
- fmt=".2f": Menampilkan angka dengan 2 angka desimal
- plt.title('Correlation Heatmap'): Memberi judul pada grafik.
- plt.show(): Menampilkan plot di layar.

```python
numeric_cols = ['Age', 'Billing Amount', 'Room Number']
corr = filtered_df[numeric_cols].corr()

print("\nMatriks Korelasi:")
print(corr)
plt.figure(figsize=(8,6))
sns.heatmap(corr, annot=True, cmap='RdBu', fmt=".2f")
plt.title('Correlation Heatmap')
plt.show()
```
