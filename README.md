# Quiz 1 Struktur Data

## 1. Karakteristik Memori dan Akses Data

>Jelaskan mengapa operasi akses elemen pada Array dapat dilakukan dalam waktu konstan O(1),
sedangkan pada Singly Linked List membutuhkan waktu linear O(n).
Hubungkan jawaban Anda dengan konsep alamat memori (kontinu vs non-kontinu).
---

Operasi akses elemen pada **Array** dapat dilakukan dalam waktu konstan **O(1)** karena elemen-elemen array disimpan di **memori yang kontinu (berurutan)**. Dengan struktur ini, komputer dapat langsung menghitung alamat elemen yang ingin diakses menggunakan rumus berdasarkan **base address** dan indeks, sehingga tidak perlu melakukan penelusuran dari awal.

Sebaliknya, pada **Singly Linked List**, elemen-elemen disimpan di **memori yang tidak kontinu (tersebar)** dan setiap elemen hanya terhubung melalui pointer ke elemen berikutnya. Karena tidak ada hubungan alamat langsung antar indeks, untuk mengakses elemen tertentu harus dimulai dari node pertama (head) lalu menelusuri satu per satu sampai elemen yang dituju. Proses penelusuran inilah yang menyebabkan waktu akses menjadi **O(n)**.

## 2. Analisis Efisiensi Operasi Manipulasi
>Dalam kondisi apa sebuah Linked List lebih diunggulkan dibandingkan Array untuk operasi penyisipan (insertion) dan penghapusan (deletion) data? Berikan alasan teoritisnya.
---

Linked List lebih diunggulkan dibandingkan Array untuk operasi **penyisipan (insertion)** dan **penghapusan (deletion)** ketika operasi tersebut sering dilakukan di posisi selain akhir (misalnya di awal atau di tengah struktur data), atau ketika ukuran data sering berubah dinamis.

## Alasan teoritisnya:

### 1. Tidak perlu pergeseran elemen

Pada **Array**, data disimpan secara **kontinu**, sehingga ketika terjadi:

* **Insertion di tengah/awal**, semua elemen setelahnya harus digeser ke kanan.
* **Deletion di tengah/awal**, semua elemen setelahnya harus digeser ke kiri.

Akibatnya kompleksitasnya menjadi **O(n)**.

### 2. Linked List hanya mengubah pointer

Pada **Linked List**, elemen disimpan secara **non-kontinu** dan dihubungkan dengan pointer.

* **Insertion**: cukup mengubah pointer node sebelum dan sesudah posisi sisipan.
* **Deletion**: cukup melewati (skip) node yang dihapus dengan mengubah pointer node sebelumnya.

Jika posisi sudah diketahui, operasi ini bisa dilakukan dalam **O(1)**.

## 3. Konsep Doubly Linked List
>Jelaskan struktur anatomi dari sebuah node pada Doubly Linked List. Apa dampak keberadaan pointer tambahan tersebut terhadap penggunaan memori serta fleksibilitas penelusuran dibandingkan dengan Singly Linked List?
---
Node pada **Doubly Linked List** memiliki struktur anatomi yang terdiri dari tiga bagian, yaitu **prev**, **data**, dan **next**, yang dapat digambarkan sebagai:

```
[ prev | data | next ]
```

Secara konsep, **data** menyimpan nilai, **next** menunjuk ke node berikutnya, dan **prev** menunjuk ke node sebelumnya sehingga setiap node saling terhubung dua arah. Penambahan pointer `prev` ini membuat penggunaan memori lebih besar dibanding **Singly Linked List**, tetapi memberikan keuntungan berupa fleksibilitas penelusuran dua arah serta kemudahan dalam operasi seperti penghapusan node.

Pointer tambahan (`prev`) pada **Doubly Linked List** membuat setiap node menyimpan satu pointer lebih banyak dibanding **Singly Linked List**, sehingga penggunaan memori menjadi lebih besar karena ada overhead tambahan di setiap node.

Namun, keberadaan pointer tersebut meningkatkan fleksibilitas penelusuran, karena Doubly Linked List dapat dilalui dalam **dua arah (maju dan mundur)**. Selain itu, operasi seperti penghapusan atau penyisipan pada node tertentu menjadi lebih mudah karena node sebelumnya dapat diakses langsung melalui pointer `prev`, tanpa harus menelusuri dari awal seperti pada Singly Linked List.

## 4. Mekanisme Circular Linked List
>Apa yang membedakan Circular Linked List dari Linked List biasa secara teoritis? Sebutkan satu contoh skenario penggunaan (use case) di mana struktur melingkar ini lebih
efektif digunakan.
---
Secara teoritis dalam Data Structures, **Circular Linked List** berbeda dari **Linked List biasa** karena cara node terakhir terhubung.

Pada **Linked List biasa**, setiap node menunjuk ke node berikutnya, dan node terakhir menunjuk ke `NULL`. Ini menandakan bahwa struktur data memiliki akhir yang jelas, sehingga proses traversal berhenti saat mencapai `NULL`.

Sedangkan pada **Circular Linked List**, node terakhir tidak menunjuk ke `NULL`, tetapi kembali menunjuk ke node pertama (head). Akibatnya, struktur ini membentuk lingkaran tertutup tanpa akhir yang alami. Traversal tidak berhenti karena `NULL`, tetapi harus dihentikan secara manual, misalnya ketika sudah kembali ke node awal.

Perbedaan ini membuat linked list biasa lebih cocok untuk data yang bersifat linear dengan akhir yang jelas, sedangkan circular linked list lebih cocok untuk proses yang berulang terus-menerus.

Contoh use case yang tepat untuk circular linked list adalah **playlist musik dengan mode repeat (loop)**, setiap lagu dihubungkan secara berurutan, dan lagu terakhir akan kembali ke lagu pertama. Dengan struktur circular, sistem dapat terus memutar lagu berikutnya tanpa perlu kembali secara manual ke awal playlist, karena aliran sudah otomatis membentuk siklus.

## 5. Array Dinamis di Python
>Python list secara internal diimplementasikan sebagai Dynamic Array. Jelaskan mekanisme yang terjadi ”di balik layar” ketika sebuah Dynamic Array kehabisan kapasitas saat
melakukan operasi append.
---
Python list menggunakan **dynamic array** di mana ukuran kapasitasnya bisa bertambah otomatis.

Saat melakukan `append()` dan kapasitas array sudah penuh, Python tidak menambah satu slot saja, tetapi melakukan proses **resizing**. Python akan membuat array baru dengan ukuran yang lebih besar (biasanya beberapa kali lipat dari kapasitas sebelumnya), lalu menyalin semua elemen dari array lama ke array baru secara berurutan. Setelah itu, array lama dilepas, dan elemen baru dimasukkan ke array yang baru dibuat.

Proses ini memang memakan waktu karena harus menyalin seluruh elemen, tetapi jarang terjadi. Karena Python menggunakan strategi pertumbuhan kapasitas yang besar, operasi `append()` secara rata-rata tetap efisien dengan kompleksitas **amortized O(1)**.


