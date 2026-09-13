## 🗝️ Penanganan: 4 Opsi


| Opsi | Kapan |
|------|-------|
| **Hapus** | Yakin itu error (Distance 500, Price negatif) |
| **Capping / Winsorize** | Nilai sah tapi ekstrem; batasi ke persentil (mis. p1-p99) |
| **Transformasi** (log, sqrt) | Distribusi skewed berat; kompres ekornya |
| **Biarkan** | Model tahan outlier (tree-based), atau outlier justru target analisis (fraud!) |

**Code:**
```python
# Capping ke persentil 1-99
p1, p99 = df["Price"].quantile([0.01, 0.99])
df["Price_capped"] = df["Price"].clip(lower=p1, upper=p99)

# Transformasi log (log1p aman untuk nilai 0)
df["Price_log"] = np.log1p(df["Price"])

print(df[["Price", "Price_capped", "Price_log"]].describe().round(2).T)
```

**Output:**
```bash
count        mean        std        min        25%        50%  \
Price         13580.0  1075684.08  639310.72   85000.00  650000.00  903000.00   
Price_capped  13580.0  1067605.69  594811.20  300000.00  650000.00  903000.00   
Price_log     13580.0       13.75       0.53      11.35      13.38      13.71   

                    75%         max  
Price         1330000.0  9000000.00  
Price_capped  1330000.0  3338150.00  
Price_log          14.1       16.01
```