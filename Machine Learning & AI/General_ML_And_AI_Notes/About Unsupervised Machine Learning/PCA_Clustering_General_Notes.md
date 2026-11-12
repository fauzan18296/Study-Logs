# 📝 Panduan Lengkap: Strategi Split Data, PCA, dan Model Clustering

Dokumen ini berisi panduan teoretis beserta implementasi kode Python untuk melakukan reduksi dimensi menggunakan PCA yang dilanjutkan dengan pemodelan *Clustering* tanpa merusak objektivitas evaluasi data (*Data Leakage*).

---

## 📌 1. Konsep Dasar Split Data pada Unsupervised Learning

Dalam **unsupervised learning**, Anda **tidak selalu wajib** membagi data menjadi set latih (*train*) dan uji (*test*) karena tidak ada label target (y) yang harus diprediksi secara langsung.

### Kapan TIDAK PERLU di-split?
* **Eksplorasi Murni (EDA):** Jika tujuannya hanya mencari pola, segmen pelanggan, atau struktur tersembunyi dari seluruh data yang ada saat ini (sekali selesai).
* Tidak ada "kunci jawaban", sehingga memecah data tidak memberikan manfaat evaluasi standar.

### Kapan PERLU di-split?
* **Dimensionality Reduction (PCA, Autoencoders):** Untuk mengukur *reconstruction error* pada data uji guna melihat seberapa baik model menggeneralisasi informasi.
* **Anomaly Detection (Isolation Forest):** Menguji skor anomali pada data baru yang belum pernah dilihat model.
* **Evaluasi Ground Truth:** Jika memiliki label asli yang sengaja disembunyikan untuk keperluan *benchmark* validasi.

---

## 🔍 2. Aturan Split Data Khusus untuk PCA

**PCA tidak wajib di-split** jika hanya digunakan untuk visualisasi (2D/3D) atau analisis eksploratif. Namun, aturan berubah drastis berdasarkan tujuan penggunaan:

### ⚠️ Kapan PCA WAJIB di-split?
Anda wajib melakukan *train-test split* **sebelum** menjalankan PCA jika **hasil komponen utamanya (PC1, PC2, dst.) akan dimasukkan ke dalam model Machine Learning lain (baik Supervised maupun Clustering Produksi).**

> 🔴 **Risiko Fatal: Data Leakage (Kebocoran Data)**
> Jika PCA diterapkan pada seluruh data sebelum di-split, model akan "mengintip" nilai rata-rata (*mean*) dan varians dari data uji sejak awal. Hal ini membuat evaluasi model menjadi bias, tidak objektif, dan terkesan terlalu bagus (*overoptimistic*).

---

## 🎯 3. Studi Kasus: Kombinasi PCA + Clustering

Ketika Anda menggabungkan PCA dan Model Clustering (seperti K-Means atau DBSCAN), keputusan *split data* bergantung pada 2 skenario berikut:

| Aspek | Skenario A: Analisis / Segmentasi Sekali Selesai | Skenario B: Model Produksi / Aplikasi |
| :--- | :--- | :--- |
| **Kebutuhan Split** | **TIDAK PERLU** di-split | **WAJIB** di-split (*Train* & *Test*) |
| **Tujuan** | Mengelompokkan data historis yang ada saat ini untuk keperluan laporan/strategi jangka pendek. | Membuat sistem/aplikasi yang nantinya akan terus menerima data baru di masa depan. |
| **Alasan** | Tidak ada data baru yang perlu diprediksi posisinya. Fokus pada visualisasi dan efisiensi dimensi. | Menghindari *Data Leakage* agar model dapat memprediksi klaster data baru secara adil dan objektif. |

---

## 📈 4. Tahap Awal: Menentukan Jumlah Komponen PCA (Explained Variance)

Sebelum mengunci jumlah dimensi baru, kita harus membuat **Scree Plot** untuk melihat berapa banyak informasi (varians) yang berhasil dipertahankan oleh setiap komponen utama (PC). Target umum kita adalah mempertahankan **80% hingga 95%** total varians asli.

```python
import numpy as np
import matplotlib.pyplot as plt
from sklearn.decomposition import PCA
from sklearn.preprocessing import StandardScaler
from sklearn.model_selection import train_test_split

# 1. Split Data di Awal (Asumsi df_features adalah dataset Anda)
X_train, X_test = train_test_split(df_features, test_size=0.2, random_state=42)

# 2. Standarisasi data (Wajib sebelum PCA)
scaler = StandardScaler()
X_train_scaled = scaler.fit_transform(X_train)

# 3. Fit PCA dengan semua komponen untuk melihat tren
pca_full = PCA()
pca_full.fit(X_train_scaled)

# 4. Hitung kumulatif varians
cumulative_variance = np.cumsum(pca_full.explained_variance_ratio_)

# 5. Membuat Scree Plot
plt.figure(figsize=(8, 5))
plt.plot(range(1, len(cumulative_variance) + 1), cumulative_variance, marker='o', linestyle='--', color='blue')
plt.axhline(y=0.85, color='r', linestyle='-', label='Target Informasi 85%') # Garis bantu target

plt.title('Scree Plot: Kumulatif Explained Variance', fontsize=12, fontweight='bold')
plt.xlabel('Jumlah Komponen Utama (PCs)')
plt.ylabel('Kumulatif Rasio Varians Terjelaskan')
plt.xticks(range(1, len(cumulative_variance) + 1))
plt.legend(loc='lower right')
plt.grid(True, alpha=0.3)
plt.show()
```

### Cara Membaca Grafik Scree Plot:
* **Metode Batas (Threshold):** Cari titik pada grafik garis biru yang pertama kali menyentuh atau melewati garis target merah (misal 85%). Jika titik tersebut sejajar dengan angka 3 di sumbu X, pilih **3 komponen**.
* **Metode Siku (Elbow):** Cari titik di mana grafik mulai melambat kenaikannya (membentuk siku). Kenaikan yang landai menandakan penambahan komponen setelahnya sudah tidak menyumbang informasi yang signifikan.

---

## 🔢 5. Tahap Kedua: Menentukan Jumlah Klaster Optimal (Silhouette Score)

Setelah mengunci jumlah komponen PCA (misal dipilih 2 komponen agar bisa divisualisasikan), kita mencari jumlah klaster (K) terbaik menggunakan **Silhouette Score**. Skor berkisar antara **-1 hingga +1**, di mana nilai tertinggi mendekati +1 menunjukkan pemisahan kelompok yang paling optimal.

```python
from sklearn.cluster import KMeans
from sklearn.metrics import silhouette_score

# Terapkan PCA dengan komponen terpilih (Contoh: 2 Komponen)
pca_final = PCA(n_components=2)
X_train_pca = pca_final.fit_transform(X_train_scaled)

# Uji coba beberapa nilai K (Jumlah Klaster)
range_n_clusters = [2, 3, 4, 5, 6]
silhouette_scores = []

for n_clusters in range_n_clusters:
    clusterer = KMeans(n_clusters=n_clusters, random_state=42)
    cluster_labels = clusterer.fit_predict(X_train_pca)
    
    score = silhouette_score(X_train_pca, cluster_labels)
    silhouette_scores.append(score)
    print(f"Untuk K = {n_clusters}, Silhouette Score adalah: {score:.4f}")

# Visualisasi grafik Silhouette Score vs K
plt.figure(figsize=(8, 4))
plt.plot(range_n_clusters, silhouette_scores, marker='o', color='purple', linewidth=2)
plt.title('Grafik Analisis Silhouette Score', fontsize=12, fontweight='bold')
plt.xlabel('Jumlah Klaster (K)')
plt.ylabel('Rata-rata Silhouette Score')
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()
```

### Cara Membaca Grafik Garis Silhouette:
* Cari titik puncak tertinggi untuk menentukan nilai K terbaik.
* **Skor > 0.5:** Klaster terpisah dengan sangat jelas.
* **Skor 0.25 - 0.5:** Klaster terbentuk baik namun ada sedikit bagian yang tumpang tindih di perbatasan.
* *Catatan:* Jika Anda menggunakan visualisasi tingkat lanjut (*Silhouette Plot* berbentuk balok horizontal), pastikan ketebalan balok seimbang antar klaster dan tidak ada area balok yang bernilai negatif (berada di sebelah kiri angka 0), karena nilai negatif mengindikasikan adanya data yang salah masuk klaster.

---

## 💻 6. Alur Final: Implementasi Produksi Lengkap & Visualisasi 2D

Berikut adalah alur akhir setelah Anda mengunci jumlah komponen PCA (misal: 2) and jumlah klaster (misal: 3) berdasarkan evaluasi grafik di atas. Tahap ini menyertakan proses prediksi data uji serta visualisasinya.

```python
import pandas as pd
import seaborn as sns

# ==========================================
# 1. FINAL TRAINING DENGAN PARAMETER TERPILIH
# ==========================================
kmeans_final = KMeans(n_clusters=3, random_state=42)
kmeans_final.fit(X_train_pca)  # Model belajar menentukan pusat klaster (centroids)

# ==========================================
# 2. PROSES DATA UJI SECARA OBJEKTIF (TANPA DATA LEAKAGE)
# ==========================================
# Terapkan transformasi yang sudah dipelajari dari data latih (JANGAN gunakan .fit() lagi!)
X_test_scaled = scaler.transform(X_test) 
X_test_pca = pca_final.transform(X_test_scaled)

# Prediksi klaster data baru / data uji
test_cluster_labels = kmeans_final.predict(X_test_pca) 

# ==========================================
# 3. VISUALISASI HASIL CLUSTERING (DATA LATIH)
# ==========================================
df_visual = pd.DataFrame(X_train_pca, columns=['PC1', 'PC2'])
df_visual['Cluster'] = kmeans_final.labels_
centroids = kmeans_final.cluster_centers_

plt.figure(figsize=(10, 6))
sns.scatterplot(
    x='PC1', y='PC2', 
    hue='Cluster', 
    palette='Set2', 
    data=df_visual, 
    alpha=0.8
)

# Plot koordinat Centroid (Pusat Klaster)
plt.scatter(
    centroids[:, 0], centroids[:, 1], 
    marker='X', 
    s=200, 
    color='black', 
    label='Centroids'
)

plt.title('Visualisasi Klaster K-Means pada Ruang PCA (2D)', fontsize=14, fontweight='bold')
plt.xlabel('Komponen Utama 1 (PC1)')
plt.ylabel('Komponen Utama 2 (PC2)')
plt.legend()
plt.grid(True, linestyle='--', alpha=0.5)
plt.show()
```

---

## 💡 Ringkasan Alur Kerja Validasi
1. **Split Data Awal:** Mengunci data uji agar distribusinya tidak mengintervensi pembuatan model.
2. **Scree Plot PCA:** Menentukan berapa jumlah fitur/komponen utama (PC) terbaik untuk mempertahankan informasi penting.
3. **Analisis Silhouette:** Menemukan jumlah kelompok (K) yang paling masuk akal secara matematis.
4. **Transform & Predict Data Uji:** Memasukkan data baru menggunakan aturan *scaler*, PCA, dan *Centroid* yang murni dipelajari dari data latih.
