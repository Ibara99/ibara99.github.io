# Evaluasi

Data yang digunakan merupakan data dari [Jurnal Online](https://garuda.ristekdikti.go.id) berupa paper dari 9 jurnal berbeda, dengan masing-masing jurnal didapat 10 paper. Total data yang digunakan sebanyak 90 judul dan abstrak. 

Pada percobaan ini digunakan model Fuzzy C-Means, dengan percobaan cluster dilakukan berulang kali dengan mengubah nilai parameter, yaitu Threshold untuk Seleksi Fitur, Jumlah Cluster, serta banyak N-gram. Maka dihasilkan nilai Shilhouette Coeffisient sebagai Berikut:

## Tanpa dilakukan preprocessing

Pada percobaan ini, data tidak dilakukan Seleksi Fitur apapun. Data langsung dibuat model Cluster menggunakan Fuzzy C-Means. Percobaan dilakukan beberapa kali dengan mengubah jumlah Cluster, dengan rentang 2-5.

| Jumlah Cluster | Shilhouette Coeffisien |
| -------------- | ---------------------- |
| 2              | 0.325                  |
| 3              | 0.325                  |
| 4              | 0.325                  |
| 5              | 0.325                  |

Dari hasil di atas, dapat disimpulkan, apabila tidak dilakukan tahap Seleksi Fitur, banyak cluster tidak berpengaruh pada hasil cluster tersebut. 

## Berdasarkan Jumlah Cluster

Jumlah Cluster berpengaruh dalam menentukan sebanyak apa kelompok yang akan dibuat. Hal ini diharapkan kita bisa menentukan Jumlah Cluster yang paling tepat dalam menentukan model untuk kasus ini.

Pada percobaan ini, nilai Threshold pada seleksi Fitur *Pearson* sebesar 0.8. Percobaan dilakukan sebanyak 9 kali, dengan mengubah parameter *c* pada C-Means dengan rentang 2-5. Hasilnya sebagai berikut:

| Jumlah Cluster | Shilhouette Coeffisient |
| -------------- | ----------------------- |
| 2              | 0.199                   |
| 3              | 0.057                   |
| 4              | 0.093                   |
| 5              | 0.050                   |

Dari sini bisa kita melihat bahwa *jumlah cluster 2* memiliki nilai coefisien tertinggi dengan nilai Shilhouette 0.199. Sebaliknya, cluster yang paling tidak tepat, apabila jumlah cluster sebanyak 5 dengan nilai shilhouette 0.050.

## Berdasarkan nilai Threshold

Nilai Threshold berfungsi untuk menentukan seberapa banyak fitur-fitur yang akan dihapus. Dengan dilakukan percobaan ini, diharapkan bisa menentukan nilai Threshold yang paling cocok. 

Nilai Threshold yang digunakan merupakan {0.9, 0.85, 0.8, 0.75, 0.7}. Melihat Percobaan sebelumnya, Jumlah Cluster yang paling baik merupakan 2, maka, digunakan C=2. Hasilnya didapatkan :

| Nilai Threshold | Shilhouette Coeffisient |
| --------------- | ----------------------- |
| 0.9             | 0.334                   |
| 0.85            | 0.342                   |
| 0.8             | 0.199                   |
| 0.75            | 0.255                   |
| 0.7             | 0.282                   |

Nilai Shilhouette paling tinggi didapat ketika nilai Threshold 0.85, yaitu 0.342. Selanjutnya, secara berturut-turut, 0.9, 0.7, 0.75, dan nilai terendah 0.8, yaitu 0.199.

## Berdasarkan N-Gram

N-Gram berfungsi untuk menentukan banyaknya kata per tokenisasi.  Hal ini diharapkan untuk mengetahui N-gram terbaik.

Pada percobaan ini, digunakan jumlah cluster sebanyak 2. Percobaan dilakukan sebanyak 3 kali dengan mengubah parameter "n" pada N-gram. Maka didapat:

| n-gram | Shilhouette Coeffisient |
| ------ | ----------------------- |
| 1      | 0.325                   |
| 2      | 0.176                   |
| 3      | 0.205                   |

Dari hasil di atas, didapat nilai shilhouette tertinggi dengan n-gram 1, yaitu 0.325. Sementara paling rendah adalah 0.176, apabila nilai n-gram adalah 2. 

Selain itu, apabila dilakukan seleksi fitur, `ngram > 1`  akan menghasilkan 1 cluster, tidak peduli berapapun jumlah cluster yg ditentukan.

## K-Means

Karena nilai Shilhouette yang relatif kecil, hasil dari Fuzzy C-Means akan dibandingkan dengan metode lain, yaitu K-Means, untuk melihat manakah yang lebih baik. 

Parameter yang digunakan di antaranya, Jumlah Cluster = 2, Threshold = 0.85, dan N-Gram = 1. Maka, diperoleh hasil berikut:

| Metode        | Shilhouette Coefisient |
| ------------- | ---------------------- |
| Fuzzy C-Means | 0.342                  |
| K-Means       | 0.430                  |

# Kesimpulan

Dari hasil percobaan di atas, dapat disimpulkan bahwa metode yang terbaik adalah K-Means, dengan parameter, n-gram=1, jumlah cluster=2, dan nilai Treshold=0.85.
