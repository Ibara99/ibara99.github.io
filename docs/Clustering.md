Clustering merupakan pengelompokan data menjadi k-kelompok (dengan k merupakan banyak kelompok). Pengelompkan tersebut berdasarkan ciri yang mirip. Pada kasus ini, maka ciri yang mirip bisa diketahui dari kata yang menjadi ciri dari setiap dokumen.

Metode Clustering sendiri ada banyak. Salah duanya adalah K-Means Clustering dan Fuzzy C-Means Clustering.

Setelah dilakukan proses Clustering, perlu kita cari nilai Silhouette Coefficient untuk melihat apakah hasil cluster tersebut sudah bagus atau tidak.

### K-Means

```python
# Clustering
kmeans = KMeans(n_clusters=5, random_state=0).fit(tfidf_matrix.todense())

for i in range(len(kmeans.labels_)):
    print("Doc %d =>> cluster %d" %(i+1, kmeans.labels_[i]))
```

Code di atas adalah code untuk melakukan clustering. Pada contoh ini cluster dibagi menjadi 5. Banyak cluster bisa diubah sesuai kebutuhan.

### Fuzzy C-Means

```python
cntr, u, u0, distant, fObj, iterasi, fpc = fuzz.cmeans(tfidf.T, 3, 2, 0.00001, 1000)
membership = np.argmax(u, axis=0)
```

parameter dari fuzzy c-means berturut-turut : data, jumlahCluster, pembobot, erorMaksimal, serta IterasiMaksimal.

### Shilhouette Coefisient

Shilhouette Coefisient merupakan salah satu metode evaluasi yang digunakan untuk model Cluster, seperti K-Means atau Fuzzy C-Means. Metode ini berfungsi untuk menguji kualitas dari cluster yang dihasilkan.  Untuk menghitung nilai silhoutte coefisient diperlukan jarak antar dokumen dengan menggunakan rumus *EuclideanDistance*. Setelah itu tahapan untuk menghitung nilai silhoutte coeffisien adalah sebagai berikut :

1. Untuk setiap objek i, hitung rata-rata jarak dari objek i dengan  seluruh objek yang berada dalam satu cluster. Akan didapatkan nilai  rata-rata yang disebut a*i*.

2. Untuk setiap objek i, hitung rata-rata jarak dari objek i dengan  objek yang berada di cluster lainnya. Dari semua jarak rata-rata  tersebut ambil nilai yang paling kecil. Nilai ini disebut b*i*.

3. Setelah itu maka untuk objek i memiliki nilai *silhoutte coefisien* :

   ![rumus Shilhouette](.\img\rumus_shilhouette.PNG)

Hasil perhitungan nilai silhoutte coeffisien dapat bervariasi antara -1 hingga 1. Hasil clustering dikatakan baik jikai nilai silhoutte coeffisien bernilai positif. Maka dapat dikatakan, jika s*i* = 1 berarti objek *i* sudah berada dalam cluster yang tepat. Jika nilai s*i* = 0 maka objek *i* berada di antara dua cluster sehingga objek tersebut tidak jelas harus dimasukan ke dalam cluster A atau cluster B. Akan tetapi, jika s*i* = -1 artinya struktur cluster yang dihasilkan overlapping, sehingga objek *i* lebih tepat dimasukan ke dalam cluster yang lain. 

Nilai rata-rata silhoutte coeffisien dari tiap objek dalam suatu cluster adalah suatu ukuran yang menunjukan seberapa ketat data dikelompokan dalam cluster tersebut.
