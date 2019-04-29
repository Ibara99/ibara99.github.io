Web  Crawler  adalah  sebuah  program  yang  melintasistruktur  hypertext  dari  web,  dimulai  dari  sebuah  alamatawal (yang disebut seed) dan secara sekursif mengunjungi alamat  web  di  dalam  halaman  web.   Web  Crawler  juga dikenal sebagai web robot, spider, worm, walker dan wanderer.  Semua search engine besar menggunakan crawleryang mampu melintasi internet secara terus-menerus, untuk  menemukan  dan  mengambil  halaman  web  sebanyakmungkin.  Data-data tersebut bisa sangat bervariasi, seperti text, citra, audio, video dan lain sebagainya. Dalam program ini, kita akan melakukan crawling pada text, atau lebih dikenal dengan *text Mining* .

Berikut code untuk melakukan Crawling[^1]:

```python
def crawl(src):
	global c
    page = requests.get(src)

    # Mengubah html ke object beautiful soup
    soup = BeautifulSoup(page.content, 'html.parser')

    # Find all item
    items = soup.findAll(class_='article-item')

    #print ('Proses : %.2f' %((c/maxPage)*100) + '%'); c+=1
    for item in items:
        judul = item.find(class_='title-article').getText()
        authors = item.find(class_="author-article").findAll(class_='title-author')
        author = ''
        for i in authors: author = author+i.getText()+'; '
        abstrack = item.find(class_='article-abstract').find('p').getText()

        #pengecekan data redundant
        cursor = conn.execute('select * from jurnal2 where judul=?', (judul,))
        cursor = cursor.fetchall()
        if (len(cursor) == 0):
            conn.execute("INSERT INTO jurnal2 \
                        VALUES (?, ?, ?, ?)", (judul, author, abstrack, kategori));
```

**Perlu diingat bahwa, setiap web memiliki struktur html yang berbeda**, maka jika kalian mengubah url web, maka perlu dilakukan penyesuaian pada code.

Selanjutnya, mari kita bahas lebih detail lagi. Untuk mendapatkan tag html .yang diinginkan BeautifulSoup menyediakan 2 fungsi, yaitu :

* soup.find(parameter)

  digunakan untuk mendapatkan *satu* tag html yang muncul pertama kali. Hasilnya berupa objek `soup`

* soup.findAll(parameter)

  digunakan untuk mendapatkan *semua* tag html tersebut. Hasilnya berupa `list`

Sementara itu, untuk parameternya memiliki 3 macam. Kalian bisa mencari berdasarkan:

* tag html (seperti `<p>`, `<div>`, `h1` dsb). 

  contoh: 

  code html `<div><p>aku makan sayur</p></div>`

  maka, untuk mendapatkan tag p adalah : `soup.find("p")`

* class

code html `<div><p class='makan'>aku makan sayur</p></div>`

maka, untuk mendapatkan tag p adalah : `soup.find(class_='makan')`

* id

code html `<div><p id='sayur'>aku makan sayur</p></div>`

maka, untuk mendapatkan tag p adalah : `soup.find(id='sayur')`



Lalu, untuk mendapatkan textnya, digunakan `.getText()` pada objek BeautifulSoup.

Setelah kalian paham tentang bagaimana menggunakan library beautifulsoup, kita akan membahas bagaimana code di atas bekerja.

```python
items = soup.findAll(class_='article-item')
```

Hal pertama yang kita lakukan adalah menentukan apa saja yang akan kita ambil. Pada kasus jurnal online ini, kita hanya akan mengambil judul, penulis, beserta abstraknya saja. Untuk itu, di sini kita mengambil semua paper, yang bisa kita lihat berada di class 'article-item'. 

```python
	for item in items:
        judul = item.find(class_='title-article').getText()
        authors = item.find(class_="author-article").findAll(class_='title-author')
        author = ''
        for i in authors: author = author+i.getText()+'; '
        abstrack = item.find(class_='article-abstract').find('p').getText()
```

Kemudian, untuk setiap paper, kita ambil judul (dengan class 'title-article'), penulis (dengan class 'author-article'), dan abstrak (dengan class 'article-abstract', lantas dicari tag p).

```python
		#pengecekan data redundant
        cursor = conn.execute('select * from jurnal2 where judul=?', (judul,))
        cursor = cursor.fetchall()
        if (len(cursor) == 0):
            conn.execute("INSERT INTO jurnal2 \
                        VALUES (?, ?, ?, ?)", (judul, author, abstrack, kategori));
```

Kemudian, memasukkan ke dalam database. Sebelum itu, perlu dilakukan pengecekan apakah ada data yang sama. Karena hal itu bisa mengganggu hasil akhir nanti.

[^1]:t