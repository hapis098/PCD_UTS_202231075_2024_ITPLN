
nama: hafidz nur raihan
nim : 202231075

# Project no1
1. Impor library:

import cv2
import matplotlib.pyplot as plt

#Di sini, kita mengimpor dua pustaka: OpenCV (cv2) untuk pengolahan gambar dan Matplotlib (matplotlib.pyplot) untuk visualisasi data.

2. Baca Gambar:
image = cv2.imread('citraBagas.jpg')

#Gambar dengan nama 'citraBagas.jpg' dibaca menggunakan OpenCV dan disimpan dalam variabel gambar.

3. Ubah Warna Gambar ke BGR dan RGB:
image_RGB = cv2.cvtColor(gambar, cv2.COLOR_BGR2RGB)

#Gambar diubah ke skema warna RGB menggunakan OpenCV. Konversi ini penting karena OpenCV menggunakan skema warna BGR secara default, sedangkan Matplotlib menggunakan skema warna RGB.

4. Pisahkan Saluran Warna:
red_channel = image_RGB[:,:,0]
green_channel = image_RGB[:,:,1]
blue_channel = image_RGB[:,:,2]

#Saluran warna (merah, hijau, biru) dipisahkan dari gambar RGB untuk analisis lebih lanjut.

Tampilkan Gambar Saluran Warna dalam Skala Abu-abu:
plt.figure(figsize=(15, 4))

Gambar Asli
plt.subplot(1, 4, 1)
plt.imshow(cv2.cvtColor(image_RGB, cv2.COLOR_RGB2BGR))
plt.title('Gambar Asli')
plt.axis('off')

Gambar Saluran Merah
plt.subplot(1, 4, 2)
plt.imshow(red_channel, cmap='gray')
plt.title('Saluran Merah')
plt.axis('off')

Gambar Saluran Hijau
plt.subplot(1, 4, 3)
plt.imshow(green_channel, cmap='gray')
plt.title('Saluran Hijau')
plt.axis('off')

Gambar Saluran Biru
plt.subplot(1, 4, 4)
plt.imshow(blue_channel, cmap='gray')
plt.title('Saluran Biru')
plt.axis('off')

plt.tight_layout()
plt.show()
Gambar saluran warna (merah, hijau, biru) ditampilkan dalam subplot dengan skala abu-abu menggunakan Matplotlib.

Hitung Histogram untuk Setiap Saluran Warna:
hist_red = cv2.calcHist([red_channel], [0], None, [256], [0,256])
hist_green = cv2.calcHist([green_channel], [0], None, [256], [0,256])
hist_blue = cv2.calcHist([blue_channel], [0], None, [256], [0,256])
Histogram dihitung untuk setiap saluran warna menggunakan fungsi cv2.calcHist. Ini memberikan informasi tentang distribusi intensitas piksel dalam setiap saluran warna.

Tampilkan Histogram:
plt.plot(hist_red, color='r')
plt.plot(hist_green, color='g')
plt.plot(hist_blue, color='b')
plt.title('Histogram Warna Merah, Hijau, dan Biru')
plt.xlabel('Nilai Intensitas')
plt.ylabel('Frekuensi')
plt.show()
Histogram untuk setiap saluran warna (merah, hijau, biru) ditampilkan menggunakan Matplotlib dengan warna yang sesuai. Ini membantu dalam analisis distribusi intensitas piksel dalam gambar.

Project No 2

Impor Pustaka:
import cv2
import numpy as np
import matplotlib.pyplot as plt
Pada tahap ini, kita mengimpor pustaka yang diperlukan. cv2 untuk pengolahan gambar dan visi komputer, numpy untuk manipulasi array, dan matplotlib.pyplot untuk visualisasi data.

Baca Gambar:
image = cv2.imread('citraBagas.jpg')
Gambar dengan nama 'citraBagas.jpg' dibaca menggunakan OpenCV (cv2.imread) dan disimpan dalam variabel gambar.

Ubah Warna Gambar ke Ruang Warna HSV:
hsv = cv2.cvtColor(image, cv2.COLOR_BGR2HSV)
Gambar yang telah dibaca dikonversi ke ruang warna HSV (Hue, Saturation, Value) menggunakan OpenCV.

Tentukan Rentang Warna untuk Biru, Merah, dan Hijau:
blue_lower = np.array([100, 43, 46])
blue_upper = np.array([130, 255, 255])
red_lower = np.array([160, 43, 46])
red_upper = np.array([180, 255, 255])
green_lower = np.array([36, 43, 46])
green_upper = np.array([70, 255, 255])
Rentang warna untuk biru, merah, dan hijau didefinisikan dalam format HSV. Nilai-nilai ini menentukan rentang warna yang akan dideteksi.

Buat Masker untuk Setiap Warna:
blue_mask = cv2.inRange(hsv, blue_lower, blue_upper)
red_mask = cv2.inRange(hsv, red_lower, red_upper)
green_mask = cv2.inRange(hsv, green_lower, green_upper)
Masker (gambar biner) dibuat untuk setiap warna berdasarkan rentang warna yang telah ditentukan.

Temukan Piksel yang Cocok dengan Setiap Warna:
blue_pixels = cv2.bitwise_and(image, image, mask=blue_mask)
red_pixels = cv2.bitwise_and(image, image, mask=red_mask)
green_pixels = cv2.bitwise_and(image, image, mask=green_mask)
Piksel yang cocok dengan setiap warna ditentukan dengan menggunakan operasi bitwise AND antara gambar asli dan masker warna.

Tampilkan Gambar Asli dan Hasil Deteksi Warna:
plt.figure(figsize=(10, 5))
plt.subplot(2, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title('Gambar Asli')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.imshow(cv2.cvtColor(blue_pixels, cv2.COLOR_BGR2RGB))
plt.title('Biru')
plt.axis('off')

plt.subplot(2, 2, 3)
plt.imshow(cv2.cvtColor(red_pixels, cv2.COLOR_BGR2RGB))
plt.title('Merah')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.imshow(cv2.cvtColor(green_pixels, cv2.COLOR_BGR2RGB))
plt.title('Hijau')
plt.axis('off')

plt.tight_layout()
plt.show()
Gambar asli dan gambar yang telah dideteksi untuk setiap warna (biru, merah, hijau) ditampilkan dalam subplot menggunakan Matplotlib. Gambar disertai dengan judul dan sumbu x dan y dinonaktifkan untuk memperbaiki tampilan.