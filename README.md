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

**Menampilkan Citra Asli dan Hasil Deteksi Tepi**<br>
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
### Laporan Praktikum 4<br>
### Ekstraksi Fitur  Menggunakan skimage (scikit-image) RGB to HSV<br><br>
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

***Menghitung Rata-Rata***<br>
```
mean = np.mean(img_hsv.ravel())
```
> Penjelasan:
- img_gray.ravel(): Mengubah array 2D dari gambar grayscale (img_gray) menjadi array 1D (vektor). Ini dilakukan untuk mempermudah perhitungan statistik.
- np.mean(...): Menghitung nilai rata-rata (mean) dari elemen-elemen dalam array 1D yang dihasilkan dari ravel(). Nilai mean ini merupakan rata-rata intensitas piksel dari gambar grayscale.

***Menghitung Standar Deviasi (Standard Deviation)***<br>
```
std = np.std(img_hsv.ravel())
```
> Penjelasan:
- img_gray.ravel(): Sama seperti sebelumnya, mengubah array 2D dari gambar grayscale menjadi array 1D.
- np.std(...): Menghitung nilai standar deviasi dari elemen-elemen dalam array 1D. Standar deviasi ini menunjukkan seberapa besar variasi atau penyebaran intensitas piksel di sekitar nilai mean.

***Mencetak Nilai Mean dan Standar Deviasi***<br>
```
print(mean, std)
```
> Penjelasan:
- print(mean, std): Mencetak nilai mean dan standar deviasi yang telah dihitung ke layar.

Hasil script
```
mean = np.mean(img_hsv.ravel())
std = np.std(img_hsv.ravel())

print(mean, std)
```
56.950442219440966 58.50973261678556

> Penjelasan:
- Nilai rata-rata (mean) menggambarkan intensitas piksel rata-rata dalam gambar grayscale. Dalam kasus ini, nilai rata-rata adalah 56.950442219440966.
- Standar deviasi (std) menggambarkan seberapa banyak variasi atau penyebaran intensitas piksel di sekitar nilai rata-rata. Dalam kasus ini, nilai standar deviasi adalah 58.50973261678556.
- Interpretasi Hasil
  - Mean (56.95):
    - Nilai rata-rata dari intensitas piksel dalam gambar adalah sekitar 56.95. Ini menunjukkan bahwa, secara umum, gambar tersebut cenderung memiliki intensitas piksel yang rendah, karena nilai intensitas berkisar dari 0 hingga 255 (dalam citra grayscale).
  - Standard Deviation (58.51):
    - Standar deviasi sekitar 58.51 menunjukkan bahwa ada variasi yang signifikan dalam intensitas piksel di seluruh gambar. Nilai standar deviasi yang tinggi berarti intensitas piksel tersebar luas di sekitar nilai rata-rata, menunjukkan adanya kontras atau perbedaan yang kuat antara area terang dan gelap dalam gambar.

***Gray level Co-occurrence Matrix (GLCM)***<br>
```
glcm = graycomatrix(img_v, distances=[1], angles=[0], levels=256, symmetric=True, normed=True)
```
> Penjelasan:
- graycomatrix Function:
  - Kode ini menghitung Gray Level Co-occurrence Matrix (GLCM) untuk gambar img_v. GLCM adalah matriks yang digunakan untuk menganalisis tekstur dengan mengukur seberapa sering pasangan piksel dengan nilai intensitas tertentu muncul pada jarak dan orientasi tertentu.
- Parameter Function:
  - img_v: Gambar input yang diproses. Gambar ini seharusnya dalam format grayscale, di mana nilai intensitas piksel berkisar antara 0 hingga 255.
  - distances=[1]: Jarak antara pasangan piksel yang dihitung. Dalam hal ini, jarak yang digunakan adalah 1 piksel.
  - angles=[0]: Sudut orientasi pasangan piksel yang dihitung. Dalam hal ini, sudut yang digunakan adalah 0 derajat (horizontal).
  - levels=256: Jumlah level intensitas piksel yang dipertimbangkan dalam gambar. Karena gambar adalah grayscale dengan nilai intensitas antara 0 hingga 255, jumlah level adalah 256.
  - symmetric=True: Jika True, maka GLCM akan dihitung secara simetris, yang berarti nilai (i, j) akan sama dengan (j, i). Ini berguna untuk mengurangi redundansi dalam matriks.
  - normed=True: Jika True, maka GLCM akan dinormalkan sehingga jumlah seluruh elemen dalam matriks sama dengan 1. Ini memungkinkan perbandingan matriks GLCM dari gambar yang berbeda.
- Hasil:
  - glcm: Hasil dari fungsi graycomatrix, yang merupakan matriks 4D di mana dua dimensi pertama adalah ukuran matriks GLCM, dimensi ketiga adalah untuk berbagai jarak yang digunakan, dan dimensi keempat adalah untuk berbagai sudut yang digunakan. Dalam kasus ini, hasil akan berupa matriks 256x256x1x1 karena kita menggunakan satu jarak dan satu sudut.

***Properti Tekstur Yang Dihitung dari GLCM***<br>
```
contrast = graycoprops(glcm, 'contrast')[0, 0]
dissimilarity = graycoprops(glcm, 'dissimilarity')[0, 0]
homogeneity = graycoprops(glcm, 'homogeneity')[0, 0]
energy = graycoprops(glcm, 'energy')[0, 0]
correlation = graycoprops(glcm, 'correlation')[0, 0]
ASM = graycoprops(glcm, 'ASM')[0, 0]

print(f"Contrast: {contrast}")
print(f"Dissimilarity: {dissimilarity}")
print(f"Homogeneity: {homogeneity}")
print(f"Energy: {energy}")
print(f"Correlation: {correlation}")
print(f"ASM: {ASM}")
```
> Penjelasan:
- graycoprops Function:
  - graycoprops adalah fungsi dari pustaka skimage.feature yang digunakan untuk menghitung properti tekstur dari GLCM.
- Properti Tekstur yang Dihitung:
  - Contrast: Mengukur intensitas kontras lokal dalam gambar. Nilai kontras yang tinggi menunjukkan variasi yang besar dalam intensitas piksel.
  - Dissimilarity: Mengukur seberapa banyak intensitas piksel berbeda satu sama lain. Nilai dissimilarity yang tinggi menunjukkan perbedaan intensitas yang besar.
  - Homogeneity: Mengukur kedekatan distribusi elemen GLCM ke diagonal GLCM. Nilai homogenitas yang tinggi menunjukkan tekstur yang lebih seragam.
  - Energy: Mengukur kekompakan teksur dan distribusi energi dalam GLCM. Nilai energi yang tinggi menunjukkan tekstur yang lebih seragam dan teratur.
  - Correlation: Mengukur korelasi antara pasangan piksel dalam GLCM. Nilai korelasi yang tinggi menunjukkan hubungan linier yang kuat antara piksel.
  - ASM (Angular Second Moment): Mengukur homogenitas dari gambar. ASM adalah kuadrat dari energi, sehingga memberikan informasi yang serupa dengan energi.
- Mengakses Nilai Properti:
  - Setiap properti dihitung dengan graycoprops(glcm, property_name), yang mengembalikan array 2D di mana kita hanya memerlukan nilai pertama [0, 0].
- Menampilkan Hasil:
  - Hasil dari setiap properti dicetak menggunakan print dengan format string untuk menampilkan nilai properti tersebut dengan label yang sesuai.

Hasil output script di atas menunjukkan sebagai berikut:<br>
Contrast: 344.20057390336757<br>
Dissimilarity: 8.840892650425209<br>
Homogeneity: 0.24140231347678798<br>
Energy: 0.020296884602945084<br>
Correlation: 0.9260076737518064<br>
ASM: 0.00041196352458526927<br>

> Penjelasan:
- Contrast: 344.20057390336757
  - Mengukur intensitas kontras dalam gambar. Nilai yang lebih tinggi menunjukkan kontras yang lebih besar dan perbedaan yang lebih tajam antara nilai piksel.
- Dissimilarity: 8.840892650425209
  - Mengukur seberapa berbeda pasangan piksel. Semakin tinggi nilai disimilari, semakin berbeda pasangan piksel.
- Homogeneity: 0.24140231347678798
  - Mengukur kedekatan distribusi elemen dalam GLCM ke diagonal matriks. Nilai yang lebih tinggi menunjukkan gambar yang lebih homogen.
- Energy: 0.020296884602945084
  - Mengukur keseragaman dalam GLCM. Ini adalah akar kuadrat dari jumlah kuadrat elemen dalam GLCM. Nilai yang lebih tinggi menunjukkan tekstur yang lebih seragam.
- Correlation: 0.9260076737518064
  - Mengukur korelasi antara pasangan piksel dalam GLCM. Nilai yang lebih tinggi menunjukkan bahwa piksel memiliki hubungan linier yang kuat.
- ASM: 0.00041196352458526927
  - Mengukur kekompakan dalam distribusi elemen GLCM. Ini adalah jumlah kuadrat dari elemen dalam GLCM. Nilai yang lebih tinggi menunjukkan tekstur yang lebih halus dan seragam.

