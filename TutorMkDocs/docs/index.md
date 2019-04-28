Di sini saya akan menjelaskan tentang bagaimana menggunakan MkDocs serta bagaimana menguploadnya ke Githup Pages.

## Instalasi MkDocs dan MkDocs material

Hal yang perlu dipersiapkan di sini adalah, pastikan kalian memiliki python. Lalu buka cmd (tekan Windows + R, lalu ketik cmd).

![img 1](../imgTutor/1.png)

Pastikan PC Anda terkoneksi dengan internet. Lalu lakukan hal berikut:

* Ketik `python -m pip install mkdocs`

  ![img 2](../imgTutor/2.png)

* Ketik `python -m pip install mkdocs`-material

  ![img 3](../imgTutor/3.png)

Selesai, Anda siap menggunakan MkDocs!

## Membuat Dokumentasi menggunakan MkDocs-material

Lakukan langkah-langkah di bawah ini:

* Buka CMD di direktori yang akan anda gunakan untuk membuat project MkDocs. Caranya, buka CMD seperti tadi, lalu ketik `cd Nama_Direktori`. Misalkan, Saya akan membuatnya di direktori `C:\Users\betsuni\Documents\GitHub\ibara99.github.io` maka command yang digunakan adalah sebagai berikut:

  ![Img 4](../imgTutor/4.png)

* Lalu ketikkan `python -m mkdocs new nama_folder` seperti berikut

  ![Img 5](../imgTutor/5.png)

  Maka akan muncul folder baru. Lalu pindah direktori cmd ke dalam folder tersebut dengan cara ketik `cd ./nama_folder`.

  ![Img 6](../imgTutor/6.png)

  ![Img 8](../imgTutor/7.png)

* Isi dari folder tersebut adalah sebagai berikut:

  ![Img 8](./imgTutor/8.png)

* Masukkan semua file yang ingin ditampilkan di halaman web ke folder `docs`.

  ![Img 8](../imgTutor/9.png)

* Kemudian buka file `mkdocs.yml` menggunakan text editor (NotePad atau yang lebih bagus, seperti Atom, dsb)

  ![Img 8](../imgTutor/10.png)

  ubah isi dari site_name menjadi nama website yang anda inginkan. Lalu tambahkan beberapa baris berikut:

  * `nav` berguna untuk menambahkan Navbar disebelah kiri. Strukturnya adalah:

    nav:

    - Nama_yang_Ditampilkan: Nama_File

    ![Img 11](../imgTutor/11.png)

  * Tambahkan baris theme berikut, yang berguna untuk menggunakan template material.

    ![Img 12](../imgTutor/12.png)

  * Jika Anda ingin menambahkan link ke repository Anda, tambahkan juga baris `repo_name` dan `repo_url` 

  * Jika di dalam file `.md` anda menggunakan footnote, gunakan baris berikut:

    ![Img 13](../imgTutor/13.png)

* Keseluruhan file `mkdocs.yml` adalah sebagai berikut:

  ![Img 14](../imgTutor/14.png)

* Kembali ke cmd Anda. Pastikan direktorinya berada di ./nama_file. Jika belum, lakukan langkah di atas. Jika sudah, lalu ketikkan perintah `python -m mkdocs serve`. Tunggu beberapa saat hingga muncul beberapa baris. Lalu buka web browser anda dan ketikkan url `localhost:8000`. 

  ![Img 15](../imgTutor/15.png)

  ![Img 16](../imgTutor/16.png)

* Anda tidak perlu mematikan cmd untuk mengubah file. Karena MkDocs akan dengan otomatis mengupdate tampilan apabila terdapat file yang berubah.

* Jika semua tampilan sudah benar, maka tekan CTRL+C untuk menghentikan mkdocs. Lalu ketikkan `python -m mkdocs build` untuk membuat web statis. Di direktori tersebut akan muncul folder baru bernama `site`

* MkDocs Anda siap digunakan.

## Upload ke Github Pages

Lakukan langkah-langkah berikut

* Buat Repository baru. Beri nama `username.github.io` :

  ![img 17](./imgTutor/17.png)

  *gambar terlihat eror karena saya sudah membuat repo dengan nama yang sama

* Push folder `site` ke repository tersebut:

  ![img 18](./imgTutor/18.png)

* Ketikkan link `username.github.io`di address bar untuk melihat hasilnya.

  ![img 19](./imgTutor/19.png)

* Github Pages Anda telah jadi. 

