Tahap *preprocessing* merupakan tahap mengolah data agar data lebih mudah diproses. Ada banyak jenis dari *preprocessing*. Namun, di kesempatan kali ini kita hanya akan membahas tentang seleksi fitur.

### Seleksi Fitur

Seleksi fitur merupakan salah satu cara untuk mengurangi dimensi fitur yang sangat banyak. Seperti pada kasus kita, Text Mining, jumlah fitur yang didapatkan bisa mencapai lebih dari 2000 kata yang berbeda. Namun, tidak semua kata tersebut benar-benar berpengaruh pada hasil akhir nantinya. 

Selain itu, kita tahu bahwa semakin banyak data yang diproses, maka lebih banyak biaya dan waktu yang digunakan untuk memprosesnya. Oleh karena itu,  kita perlu melakukan pengurangan fitur tanpa mengurangi kualitas hasil akhir, misalnya dengan Seleksi Fitur.

Pada dasarnya, seleksi fitur memiliki 3 tipe umum:

1. Wrap
2. Filter
3. Embed

Selain itu, Seleksi Fitur juga memiliki banyak sekali metode-metode, seperti Information Gain, Chi Square, Pearson, dll.

#### Pearson Correlation

Pendekatan Pearson merupakan pendekatan paling sederhana. Pada pendekatan ini, setiap fitur akan dihitung korelasinya. Semakin tinggi nilainya, maka fitur tersebut semakin kuat korelasinya. Lalu fitur yang memiliki korelasi tinggi akan dibuang salah satunya.

**Pendekatan ini digunakan untuk data tipe numerik**.

Codenya sebagai berikut:

```python
def pearsonCalculate(data, u,v):
    "i, j is an index"
    atas=0; bawah_kiri=0; bawah_kanan = 0
    for k in range(len(data)):
        atas += (data[k,u] - meanFitur[u]) * (data[k,v] - meanFitur[v])
        bawah_kiri += (data[k,u] - meanFitur[u])**2
        bawah_kanan += (data[k,v] - meanFitur[v])**2
    bawah_kiri = bawah_kiri ** 0.5
    bawah_kanan = bawah_kanan ** 0.5
    return atas/(bawah_kiri * bawah_kanan)
def meanF(data):
    meanFitur=[]
    for i in range(len(data[0])):
        meanFitur.append(sum(data[:,i])/len(data))
    return np.array(meanFitur)
def seleksiFiturPearson(data, threshold):
    global meanFitur
    meanFitur = meanF(data)
    u=0
    while u < len(data[0]):
        dataBaru=data[:, :u+1]
        meanBaru=meanFitur[:u+1]
        v = u
        while v < len(data[0]):
            if u != v:
                value = pearsonCalculate(data, u,v)
                if value < threshold:
                    dataBaru = np.hstack((dataBaru, data[:, v].reshape(data.shape[0],1)))
                    meanBaru = np.hstack((meanBaru, meanFitur[v]))
            v+=1
        data = dataBaru
        meanFitur=meanBaru
        if u%50 == 0 : print(u, data.shape)
        u+=1
    return data
```



#### Chi Square 

Sama seperti pendekatan pearson, hanya saja, pendekatan ini lebih digunakan untuk data tipe categorical.
