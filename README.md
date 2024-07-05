## Farrel Alfared Carasiola
## 202231003
## Pengolahan Citra Digital - A
---
### Laporan Praktikum 3<br>
### Tepi dan Garis<br><br>
***Import Library***<br>
```
import cv2 
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline

import skimage
```
> Penjelasan:
- import cv2: Mengimpor pustaka OpenCV yang digunakan untuk pemrosesan citra.
- import numpy as np: Mengimpor pustaka NumPy yang digunakan untuk operasi array.
- import matplotlib.pyplot as plt: Mengimpor pustaka Matplotlib yang digunakan untuk membuat visualisasi data.
- %matplotlib inline: Magic function di Jupyter Notebook yang digunakan untuk menampilkan plot secara langsung di notebook.
- import skimage: Mengimpor pustaka scikit-image untuk pemrosesan citra, meskipun dalam kode ini tidak digunakan.

***Membaca Citra***<br>
```
image = cv2.imread("1.jpg")
```
> Penjelasan:
- cv2.imread("1.jpg"): Membaca citra dari file '1.jpg' dan menyimpannya dalam variabel image. OpenCV membaca citra dalam format BGR (Blue, Green, Red).

***Mengubah Citra ke Grayscale***<br>
```
gray = cv2.cvtColor(image,cv2.COLOR_BGR2GRAY)
```
> Penjelasan:
- cv2.cvtColor(image, cv2.COLOR_BGR2GRAY): Mengonversi citra dari format BGR ke grayscale dan menyimpannya dalam variabel gray.

***Deteksi Tepi Menggunakan Canny***<br>
```
edges = cv2.Canny(image, 100, 150)
```
> Penjelasan:
- cv2.Canny(image, 100, 150): Menerapkan algoritma deteksi tepi Canny pada citra dengan threshold nilai 100 dan 150. Hasilnya disimpan dalam variabel edges.

***Menampilkan Citra Asli dan Hasil Deteksi Tepi***<br>
```
fig, axs = plt.subplots(1, 2, figsize=(18, 10)) 
ax = axs.ravel()
```
> Penjelasan:
- fig, axs = plt.subplots(1, 2, figsize=(18, 10)): Membuat dua subplot berdampingan dalam satu figure dengan ukuran keseluruhan 18 inci x 10 inci. fig adalah objek figure yang mewakili keseluruhan plot, dan axs adalah array dari objek subplot (axes).
- ax = axs.ravel(): Mengubah array dua dimensi axs menjadi array satu dimensi untuk mempermudah akses elemen subplot.
```
ax[0].imshow(gray, cmap="gray")
ax[0].set_title("Gambar asli")
```
> Penjelasan:
- ax[0].imshow(gray, cmap="gray"): Menampilkan citra grayscale pada subplot pertama dengan colormap grayscale.
- ax[0].set_title("Gambar Original"): Mengatur judul dari subplot pertama menjadi "Gambar asli".
```
ax[1].imshow(edges, cmap="gray")
ax[1].set_title("Gambar yg udah")
```
> Penjelasan:
- ax[1].imshow(edges, cmap="gray"): Menampilkan hasil deteksi tepi pada subplot kedua dengan colormap grayscale.
- ax[1].set_title("After Picture"): Mengatur judul dari subplot kedua menjadi "Gambar yg udah".

***Menampilkan Plot***<br>
```
plt.show()
```
> Penjelasan:
- plt.show(): Menampilkan figure yang telah dibuat dengan kedua subplot tersebut.<br>

### Overlay
***Deteksi Garis Menggunakan Hough Transform***<br>
```
lines = cv2.HoughLinesP(edges, 1, np.pi/180, 30, maxLineGap=250)
```
> Penjelasan:
- cv2.HoughLinesP(edges, 1, np.pi/180, 30, maxLineGap=250): Fungsi ini digunakan untuk mendeteksi garis dalam gambar biner (dalam hal ini, hasil deteksi tepi edges). Parameter yang digunakan:
  - edges: Gambar biner dari hasil deteksi tepi.
  - 1: Resolusi parameter rho (jarak) dalam piksel.
  - np.pi/180: Resolusi parameter theta (sudut) dalam radian.
  - 30: Ambang batas minimal untuk mendeteksi sebuah garis.
  - maxLineGap=250: Jarak maksimum antara dua titik untuk dianggap sebagai satu garis.
- Hasilnya adalah sebuah array lines yang berisi koordinat-koordinat titik awal dan akhir dari garis-garis yang terdeteksi.

***Menyalin Gambar Asli***<br>
```
image_line = image.copy()
```
> Penjelasan:
- image.copy(): Membuat salinan dari gambar asli dan menyimpannya dalam variabel image_line.

***Menggambar Garis pada Gambar***<br>
```
for line in lines:
    x1, y1, x2, y2 = line[0]
    cv2.line(image_line, (x1, y1), (x2, y2), (100, 8, 255), 1)
```
> Penjelasan:
- for line in lines:: Melakukan iterasi untuk setiap garis yang terdeteksi.
- x1, y1, x2, y2 = line[0]: Mengambil koordinat titik awal dan akhir dari garis.
- cv2.line(image_line, (x1, y1), (x2, y2), (100, 8, 255), 1): Menggambar garis pada gambar image_line dengan warna (100, 8, 255) dan ketebalan garis 1 piksel.

***Menampilkan Gambar Asli dan Gambar dengan Garis Terdeteksi***<br>
```
fig, axs = plt.subplots(1, 2, figsize=(10, 10))
ax = axs.ravel()
```
> Penjelasan:
- fig, axs = plt.subplots(1, 2, figsize=(10, 10)): Membuat dua subplot berdampingan dalam satu figure dengan ukuran keseluruhan 10 inci x 10 inci. fig adalah objek figure yang mewakili keseluruhan plot, dan axs adalah array dari objek subplot (axes).
- ax = axs.ravel(): Mengubah array dua dimensi axs menjadi array satu dimensi untuk mempermudah akses elemen subplot.

***Menampilkan Gambar Asli dan Gambar dengan Garis Terdeteksi***<br>
```
fig, axs = plt.subplots(1, 2, figsize=(10, 10))
ax = axs.ravel()
```
> Penjelasan:
- fig, axs = plt.subplots(1, 2, figsize=(10, 10)): Membuat dua subplot berdampingan dalam satu figure dengan ukuran keseluruhan 10 inci x 10 inci. fig adalah objek figure yang mewakili keseluruhan plot, dan axs adalah array dari objek subplot (axes).
- ax = axs.ravel(): Mengubah array dua dimensi axs menjadi array satu dimensi untuk mempermudah akses elemen subplot.
```
ax[0].imshow(gray, cmap="gray")
ax[0].set_title("Gambar Original")
```
> Penjelasan:
- ax[0].imshow(gray, cmap="gray"): Menampilkan gambar grayscale pada subplot pertama dengan colormap grayscale.
- ax[0].set_title("Gambar Original"): Mengatur judul dari subplot pertama menjadi "gambar asli"
```
ax[1].imshow(image_line, cmap="gray")
ax[1].set_title("After Picture")
```
> Penjelasan:
- ax[1].imshow(image_line, cmap="gray"): Menampilkan gambar dengan garis terdeteksi pada subplot kedua dengan colormap grayscale.
- ax[1].set_title("gambar yg udah"): Mengatur judul dari subplot kedua menjadi "gambar yg udah".

***Menampilkan Plot***<br>
```
plt.show()
```
> Penjelasan:
- plt.show(): Menampilkan figure yang telah dibuat dengan kedua subplot tersebut.

***Mengeksekusi Variabel***<br>
```
edges
lines
lines.shape
```
> Penjelasan:
- edges: Menampilkan gambar hasil deteksi tepi (tidak ada output yang terlihat, mungkin di Jupyter Notebook akan menampilkan array tepi).
- lines: Menampilkan array dari garis-garis yang terdeteksi.
- lines.shape: Menampilkan bentuk dari array lines, yang menunjukkan jumlah garis yang terdeteksi dan dimensi dari data (biasanya (n, 1, 4), dimana n adalah jumlah garis yang terdeteksi).

Hasil script
```
edges
```
array([[  0,   0,   0, ...,   0, 255,   0],
       [  0,   0,   0, ...,   0, 255,   0],
       [  0,   0,   0, ...,   0,   0, 255],
       ...,
       [  0, 255, 255, ...,   0, 255, 255],
       [255,   0,   0, ...,   0,   0,   0],
       [  0,   0, 255, ..., 255,   0,   0]], dtype=uint8)

> Penjelasan:
- Nilai Piksel:
  - Nilai piksel dalam array ini adalah 0 atau 255 (dtype=uint8), di mana 0 mewakili piksel yang bukan tepi dan 255 mewakili piksel yang merupakan tepi.
Dalam konteks deteksi tepi Canny, nilai 255 menunjukkan bahwa ada perubahan tajam dalam intensitas di sekitar piksel tersebut, yang biasanya menandakan adanya tepi atau batas antara dua area dengan intensitas yang berbeda.
- Visualisasi:
  - Jika array edges divisualisasikan sebagai gambar, piksel dengan nilai 255 akan muncul sebagai garis putih (tepian) pada latar belakang hitam (nilai 0), menunjukkan lokasi dari tepi-tepi dalam gambar asli.

Hasil script
```
lines
```
array([[[ 567,  796,  567,   84]],
       [[   0,  788, 1199,  767]],
       [[   0,  298, 1183,  298]],
       ...,
       [[   0,  192, 1199,  192]],
       [[ 143,  212, 1197,  212]],
       [[   1,  191, 1198,  191]]], dtype=int32)
       
> Penjelasan:
- Koordinat Garis:
  - Setiap sub-array berisi empat nilai [x1, y1, x2, y2], yang merupakan koordinat dari dua titik akhir dari garis yang terdeteksi dalam gambar.
  - Misalnya, sub-array pertama [[ 567, 796, 567, 84]] menunjukkan bahwa garis pertama dimulai dari titik (567, 796) dan berakhir pada titik (567, 84).

Hasil script
```
lines.shape
```
(545, 1, 4)
> Penjelasan:
- Dimensi Array:
  - lines.shape menghasilkan tuple (545, 1, 4).
  - Ini berarti array lines memiliki tiga dimensi.
- Rincian Dimensi:
  - Dimensi pertama (545): Menunjukkan jumlah total garis yang terdeteksi. Dalam hal ini, ada 545 garis yang terdeteksi dalam gambar.
  - Dimensi kedua (1): Ini adalah dimensi tambahan yang dihasilkan oleh fungsi OpenCV untuk menyimpan koordinat garis dalam sub-array.
  - Dimensi ketiga (4): Menunjukkan jumlah koordinat yang dibutuhkan untuk mendefinisikan setiap garis. Setiap garis diwakili oleh empat nilai koordinat [x1, y1, x2, y2].

---
### Laporan Praktikum 3<br>
### Tepi dan Garis<br><br>
***Import library***<br>
```
import cv2
import matplotlib.pyplot as plt
import numpy as np 
import skimage
from skimage.feature import graycomatrix, graycoprops
```
> Penjelasan:
- Pada bagian ini, beberapa pustaka yang diperlukan diimpor. cv2 adalah pustaka OpenCV yang digunakan untuk pemrosesan gambar. matplotlib.pyplot digunakan untuk plotting gambar. numpy digunakan untuk operasi numerik. skimage adalah pustaka dari scikit-image yang digunakan untuk pengolahan gambar.

***Membaca Gambar***<br>
```
img = cv2.imread("1.jpg")
```
> Penjelasan:
- Gambar dengan nama 1.jpg dibaca menggunakan OpenCV dan disimpan dalam variabel img.

***Konversi Gambar dari RGB ke HSV***<br>
```
img_hsv = cv2.cvtColor(img, cv2.COLOR_RGB2HSV)
```
> Penjelasan:
- Gambar yang telah dibaca dikonversi dari ruang warna RGB ke ruang warna HSV menggunakan fungsi cv2.cvtColor.

***Ekstraksi Kanal V dari Gambar HSV***<br>
```
img_v = img_hsv[:, :, 2]
```
> Penjelasan:
- Kanal V (Value) dari gambar HSV diekstraksi dan disimpan dalam variabel img_v. HSV adalah ruang warna yang terdiri dari Hue, Saturation, dan Value. Kanal V menunjukkan intensitas atau kecerahan gambar.

***Plot Gambar RGB dan HSV***<br>
```
fig, axs = plt.subplots(1, 2, figsize=(15, 10))

ax = axs.ravel()

ax[0].imshow(img)
ax[0].set_title("RGB")

ax[1].imshow(img_hsv)
ax[1].set_title("HSV")

plt.show()
```
> Penjelasan:
- fig, axs = plt.subplots(1, 2, figsize=(15, 10)): Membuat dua subplot dalam satu baris dengan ukuran keseluruhan 15x10 inci.
- ax = axs.ravel(): Mengubah array 2D axs menjadi array 1D untuk mempermudah akses.
- ax[0].imshow(img): Menampilkan gambar asli (RGB) pada subplot pertama.
- ax[0].set_title("RGB"): Memberi judul "RGB" pada subplot pertama.
- ax[1].imshow(img_hsv): Menampilkan gambar dalam ruang warna HSV pada subplot kedua.
- ax[1].set_title("HSV"): Memberi judul "HSV" pada subplot kedua.
plt.show(): Menampilkan kedua subplot tersebut.
