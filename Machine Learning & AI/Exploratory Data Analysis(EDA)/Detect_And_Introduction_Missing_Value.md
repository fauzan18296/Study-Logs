# ⚠️ Menangani Missing Values

Missing values (NaN) hampir pasti ada di data nyata. Salah menanganinya bisa membuang informasi berharga atau malah menciptakan bias. Aturan pertama: **pahami dulu kenapa datanya hilang, baru putuskan penanganannya.**

### Tiga Mekanisme Hilangnya Data

- **MCAR** (Missing Completely At Random): hilang murni acak. Paling aman ditangani.
- **MAR** (Missing At Random): hilangnya berkaitan dengan variabel lain (misal: responden muda cenderung tidak mengisi kolom penghasilan).
- **MNAR** (Missing Not At Random): hilangnya berkaitan dengan nilai itu sendiri (misal: orang bergaji tinggi enggan mengisi kolom gaji). Paling berbahaya — imputasi biasa bisa bias.

---

## 🔎 Deteksi Missing Value

- `df.isnull().sum()` — jumlah missing per kolom.
- Persentase lebih informatif daripada jumlah mentah.
- Cek juga **pola**: apakah missing di kolom A selalu barengan kolom B?

**Code:**
```python
jumlah = df_new.isnull().sum()
persen = (df_new.isnull().mean()) * 100
print(pd.DataFrame({"jumlah": jumlah, "persen": persen.round(1)}))

# Baris yang mengandung minimal satu NaN
print("\nBaris dengan NaN:", df_new.isnull().any(axis=1).sum(), "dari", len(df))
```

**Output:**
```bash
jumlah  persen
Suburb              0     0.0
Address             0     0.0
Rooms               0     0.0
Type                0     0.0
Price               0     0.0
Method              0     0.0
SellerG             0     0.0
Date                0     0.0
Distance            0     0.0
Postcode            0     0.0
Bedroom2            0     0.0
Bathroom            0     0.0
Car                62     0.5
Landsize            0     0.0
BuildingArea     6450    47.5
YearBuilt        5375    39.6
CouncilArea      1369    10.1
Lattitude           0     0.0
Longtitude          0     0.0
Regionname          0     0.0
Propertycount       0     0.0

Baris dengan NaN: 7384 dari 13580
```


