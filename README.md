# Implementation DES Algorithm ( 8 Characters only )

| Nama       | NRP   |
|------------|---------------|
| Muhammad Irfan Hakim | 5025221291 |

![image](https://github.com/user-attachments/assets/41064bd0-b616-4c4a-b47b-ccd2cb725022)

## 1. Initial Permutation (IP)
Pada tahap pertama, data yang akan dienkripsi dipecah menjadi blok-blok berukuran 64-bit. Setiap blok kemudian dipermutasikan menggunakan **Initial Permutation (IP)**, yang mengubah urutan bit sesuai aturan permutasi yang telah ditentukan.

**Tujuan:** Mengacak urutan bit untuk mempersiapkan data sebelum ronde enkripsi.

---

## 2. Pembagian Blok Menjadi L dan R
Setelah **Initial Permutation**, blok 64-bit dibagi menjadi dua bagian:
- **L (Left half)**, bagian kiri 32-bit
- **R (Right half)**, bagian kanan 32-bit

kemudian diolah selama 16 rounds dalam **struktur Feistel**, yang secara berulang menggunakan substitusi dan permutasi.

---

## 3. Proses 16 Rounds Enkripsi
DES menggunakan 16 ronde enkripsi, dimana setiap ronde menggunakan **round key** yang berbeda, yang dihasilkan dari **main key**.

### Proses Tiap Ronde:
1. **XOR Round Key:** 
   - **main key** sepanjang 56-bit digunakan untuk menghasilkan **round key** sepanjang 48-bit. Round key ini di-**XOR** dengan bagian kanan (R) dari data.

2. **Expansion (E-Box):**
   - Bagian **R** sepanjang 32-bit diperluas menjadi 48-bit dengan **expansion permutation** agar dapat di-**XOR** dengan round key yang lebih panjang.

3. **S-Box Substitution:**
   - Input 48-bit dipecah menjadi 8 blok 6-bit, kemudian setiap blok dilewatkan ke salah satu dari 8 **S-Box** untuk mendapatkan output 4-bit. Total output menjadi 32-bit.

4. **Permutation (P-Box):**
   - Output 32-bit dari S-Box diacak kembali dengan **P-Box permutation** untuk menghasilkan urutan bit yang lebih rumit.

5. **XOR dengan L (Left half):**
   - Hasil akhir di-**XOR** dengan bagian kiri (L) dan menjadi bagian kanan (R) baru untuk ronde berikutnya.

6. **L dan R Dipertukarkan:**
   - Pada setiap ronde, **L** dan **R** saling bertukar tempat.

Proses ini diulang sebanyak **16 kali**, dan setiap ronde menghasilkan data yang lebih terenkripsi.

---

## 4. Final Permutation (FP)
Setelah 16 ronde selesai, bagian **L** dan **R** akhir digabungkan kembali menjadi 64-bit. Blok data 64-bit ini kemudian dipermutasikan lagi menggunakan **Final Permutation (FP)**, yang merupakan kebalikan dari **Initial Permutation (IP)**.

**Tujuan:** Menghasilkan output yang terenkripsi dengan urutan bit yang kembali diacak.

---

## 5. Key dalam DES
DES menggunakan **Main Key 56-bit** yang dihasilkan dari key 64-bit (dengan 8 bit sebagai bit paritas). Main key ini digunakan untuk menghasilkan **round keys** unik di setiap ronde.

### Key Schedule:
- Main key dipecah menjadi dua bagian **C** dan **D** (masing-masing 28-bit).
- Pada setiap ronde, **C** dan **D** di-**shift** ke kiri sesuai **shift schedule**.
- Setelah setiap shift, **C** dan **D** digabungkan kembali dan dipermutasikan menjadi **round key 48-bit**.

---
