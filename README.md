# EDA-Healthcare-Kelompok-7

- Nadia Clearesta Shafira (103102400007)
- Zerlina Agustiya Putri (103102400009)
- Moch Rafi Nanda Prayogo (103102400002)
- Abdul Khaliq (103102400078)

## 1) Load Data

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
```python
df.info()
df.describe(include='all').T
```

# 3) Cek Nilai Duplikat dan Nilai Unik
```python
print("Jumlah duplikat:", df.duplicated().sum())
df[df.duplicated()]
df.nunique()
```

## 4) Visualisasi Jumlah Unik
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
```python
print("Nilai Null:")
df.isnull()

print("Jumlah Nilai Null per Kolom:")
df.isnull().sum()
```

## 6) Replace Semua Null Values
```python

```

## 7) Mengetahui Tipe Data dari Dataset
```python

```

## 8) Filter Data
```python

```

## 9) Create a Box Plot
```python

```

## 10) Correlation
```python

```
