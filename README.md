
# TEORI 
Teori dan materi yang sering digunakan dalam segmentasi warna untuk mendeteksi buah. Berikut adalah teori dan materi yang umumnya digunakan:

Model Warna:

Ruang Warna RGB: Ruang warna RGB (Red, Green, Blue) adalah model warna yang paling umum digunakan dalam pemrosesan gambar. Pada model ini, warna diwakili oleh kombinasi intensitas tiga kanal warna: merah (R), hijau (G), dan biru (B).
Ruang Warna HSV: Ruang warna HSV (Hue, Saturation, Value) lebih intuitif dalam representasi warna manusia. Hue (H) menggambarkan tipe warna, Saturation (S) menggambarkan kecerahan warna, dan Value (V) menggambarkan intensitas warna.
Thresholding:

Metode thresholding digunakan untuk mengubah gambar ke dalam citra biner dengan membaginya menjadi dua kelas: piksel objek dan piksel latar belakang. Thresholding dilakukan dengan membandingkan nilai piksel dengan ambang batas tertentu.
Operasi Morfologi:

Dilasi (Dilation): Operasi dilasi digunakan untuk memperluas objek dalam gambar dengan menggunakan kernel tertentu.
Erosi (Erosion): Operasi erosi digunakan untuk mengikis batas objek dalam gambar dengan menggunakan kernel tertentu.
Opening: Opening merupakan kombinasi operasi erosi dan dilasi yang berguna untuk menghapus noise dan objek kecil.
Closing: Closing merupakan kombinasi operasi dilasi dan erosi yang berguna untuk mengisi celah-celah kecil dalam objek.
Deteksi Kontur:

Deteksi kontur digunakan untuk mengidentifikasi dan mendeteksi tepi atau kontur objek dalam gambar.
Metode umum yang digunakan dalam deteksi kontur adalah metode Canny, metode Sobel, dan metode Prewitt.
Analisis dan Filterisasi:

Setelah deteksi kontur, objek-objek yang terdeteksi dapat dianalisis berdasarkan fitur-fitur seperti area, bentuk, atau warna untuk memfilter objek yang diinginkan.
Saat mengimplementasikan segmentasi warna untuk mendeteksi buah, Anda dapat menggabungkan langkah-langkah seperti konversi ruang warna, thresholding, operasi morfologi, deteksi kontur, dan analisis fitur untuk memisahkan dan mendeteksi buah dalam gambar.

# CODINGAN DAN PENJELASAN
      import cv2
      import numpy as np
      import matplotlib.pyplot as plt

      image_path = "FADLIE.jpg"

      image = cv2.imread(image_path)
      image = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

      hsv_image = cv2.cvtColor(image, cv2.COLOR_RGB2HSV)

      lower_green = np.array([35, 50, 50], dtype=np.uint8)
      upper_green = np.array([90, 255, 255], dtype=np.uint8)

      lower_red = np.array([0, 70, 70], dtype=np.uint8)
      upper_red = np.array([10, 255, 255], dtype=np.uint8)

      lower_yellow = np.array([20, 100, 100], dtype=np.uint8)
      upper_yellow = np.array([30, 255, 255], dtype=np.uint8)

      mask_red = cv2.inRange(hsv_image, lower_red, upper_red)
      mask_green = cv2.inRange(hsv_image, lower_green, upper_green)
      mask_yellow = cv2.inRange(hsv_image, lower_yellow, upper_yellow)

      result_red = cv2.bitwise_and(image, image, mask=mask_red)
      result_green = cv2.bitwise_and(image, image, mask=mask_green)
      result_yellow = cv2.bitwise_and(image, image, mask=mask_yellow)

      fig, axs = plt.subplots(1, 4, figsize=(15, 5))

      axs = axs.ravel()

      axs[0].imshow(image)
      axs[0].set_title('Original Image')
      axs[0].axis('on')
      axs[0].text(10, 10, f"({image.shape[1]}, {image.shape[0]})", color='white')

      axs[1].imshow(result_red)
      axs[1].contour(mask_red)
      axs[1].set_title('Red Fruits')
      axs[1].axis('on')
      axs[1].text(10, 10, f"({result_red.shape[1]}, {result_red.shape[0]})", color='white')

      axs[2].imshow(result_green)
      axs[2].contour(mask_green)
      axs[2].set_title('Green Fruits')
      axs[2].axis('on')
      axs[2].text(10, 10, f"({result_green.shape[1]}, {result_green.shape[0]})", color='white')

      axs[3].imshow(result_yellow)
      axs[3].contour(mask_yellow)
      axs[3].set_title('Yellow Fruits')
      axs[3].axis('on')
      axs[3].text(10, 10, f"({result_yellow.shape[1]}, {result_yellow.shape[0]})", color='white')

      # Rotate the images
      for ax in axs[1:]:
         ax.set_adjustable('box')
         ax.set_aspect('equal')
         ax.get_xaxis().set_visible(True)
         ax.get_yaxis().set_visible(True)
         ax.set_frame_on(True)
         ax.yaxis.set_label_coords(0.5, -0.1)
         ax.set_xticks([])
         ax.set_yticks([])
         ax.spines['top'].set_visible(True)
         ax.spines['right'].set_visible(True)
         ax.spines['bottom'].set_visible(True)
         ax.spines['left'].set_visible(True)
         ax.yaxis.set_ticklabels([])
         ax.xaxis.set_ticklabels([])
         ax.text(10, 10, f"({ax.get_xlim()[1]}, {ax.get_ylim()[1]})", color='white')

         ax.set_aspect('auto')

      plt.tight_layout()
      plt.show()




Berikut adalah langkah-langkah penyelesaian dari codingan di atas:

1. Mengimpor modul matplotlib.pyplot dan skimage.io untuk menampilkan gambar dan membaca gambar menggunakan scikit-image.
2. Mengimpor modul skimage.color untuk mengubah gambar ke skala keabuan.
3. Mengimpor modul skimage.measure untuk melakukan operasi pengukuran dan deteksi kontur.
4. Membuat fungsi detect_letters(image_path) untuk mendeteksi huruf-huruf dalam gambar.
5. Membaca gambar menggunakan skimage.io.imread() dan menyimpannya dalam variabel image.
6. Menampilkan gambar asli menggunakan plt.imshow().
7. Memanggil fungsi detect_letters() untuk mendapatkan persegi panjang yang mengelilingi huruf-huruf yang terdeteksi.
8. Menampilkan gambar setelah deteksi teks menggunakan plt.imshow().
9. Menggunakan loop for untuk setiap persegi panjang yang terdeteksi, membuat objek Rectangle dengan menggunakan plt.Rectangle(), dan menambahkannya ke plot menggunakan plt.gca().add_patch().
10. Menampilkan gambar yang telah dideteksi hurufnya menggunakan plt.show().

Dalam proses deteksi huruf, langkah-langkahnya adalah sebagai berikut:
- Gambar awal diubah ke skala keabuan menggunakan skimage.color.rgb2gray().
- Dilakukan thresholding untuk mengubah gambar menjadi citra biner menggunakan gray < 0.5.
- Dilakukan operasi morfologi untuk membersihkan gambar menggunakan skimage.measure.label().
- Kemudian, menggunakan skimage.measure.find_contours() untuk mencari kontur huruf pada gambar yang telah dibersihkan.
- Kontur huruf yang ditemukan dianalisis berdasarkan area dan aspek rasio untuk memfilter huruf-huruf yang dianggap valid.
- Huruf yang terdeteksi (persegi panjang yang mengelilingi huruf) disimpan dalam list detected_letters.
- Hasil akhirnya adalah gambar asli dengan persegi panjang yang mengelilingi huruf yang terdeteksi ditampilkan menggunakan plt.imshow() dan plt.show().

# JOURNAL
-