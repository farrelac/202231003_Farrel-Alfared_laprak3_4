## Farrel Alfared Carasiola
## 202231003
## Pengolahan Citra Digital - A
---
Berikut adalah Laporan Praktikum 3 dan Praktikum 4, tentang Ekstrasi Fitur Scikit-Image RGB to HSV<br><br>
***Import Library***<br>
import matplotlib.pyplot as plt
from skimage import io, color<br>
>Penjelasan:
- matplotlib.pyplot as plt: Mengimpor pustaka matplotlib yang digunakan untuk membuat visualisasi data.
- from skimage import io, color: Mengimpor modul io dan color dari pustaka skimage. Modul io digunakan untuk membaca citra, sedangkan modul color digunakan untuk konversi ruang warna.

***Membaca citra***<br>
image = io.imread('1.jpg')<br>
> Penjelasan:
- io.imread('1.jpg'): Membaca citra dari file '1.jpg' dan menyimpannya dalam variabel image. image akan berbentuk array numpy yang merepresentasikan citra tersebut dalam ruang warna RGB.

***Mengubah citra dari RGB ke HSV***<br>
hsv_image = color.rgb2hsv(image)<br>
> Penjelasan:
- color.rgb2hsv(image): Mengubah citra dari ruang warna RGB ke ruang warna HSV dan menyimpannya dalam variabel hsv_image. Ruang warna HSV (Hue, Saturation, Value) memisahkan informasi warna dari intensitas, yang seringkali lebih berguna untuk analisis citra.

***Menampilkan citra asli dan citra HSV***<br>
fig, ax = plt.subplots(1, 2, figsize=(12, 6))<br>

ax[0].imshow(image)<br>
ax[0].set_title('Citra Asli')<br>
ax[0].axis('off')<br>

ax[1].imshow(hsv_image)<br>
ax[1].set_title('Citra HSV')<br>
ax[1].axis('off')<br>

plt.show()<br>
> Penjelasan:
- fig, ax = plt.subplots(1, 2, figsize=(12, 6)): Membuat dua subplot berdampingan dalam satu figure dengan ukuran keseluruhan 12 inci x 6 inci. fig adalah objek figure yang mewakili keseluruhan plot, dan ax adalah array dari objek subplot (axes).
- ax[0].imshow(image): Menampilkan citra asli pada subplot pertama.
- ax[0].set_title('Citra Asli'): Mengatur judul dari subplot pertama menjadi 'Citra Asli'.
- ax[0].axis('off'): Mematikan tampilan sumbu pada subplot pertama sehingga sumbu x dan y tidak ditampilkan.
- ax[1].imshow(hsv_image): Menampilkan citra yang telah dikonversi ke HSV pada subplot kedua.
- ax[1].set_title('Citra HSV'): Mengatur judul dari subplot kedua menjadi 'Citra HSV'.
- ax[1].axis('off'): Mematikan tampilan sumbu pada subplot kedua sehingga sumbu x dan y tidak ditampilkan.
- plt.show(): Menampilkan figure yang telah dibuat dengan kedua subplot tersebut.
