# OS Kuis 2 — Pemrograman Bash, Manajemen Memori & File

Kuis ini mencakup skrip Bash (Bab 7), manajemen memori (Bab 8), dan manajemen file/pengguna (Bab 9).

Setiap soal adalah skrip bash yang membaca dari **stdin** dan menulis ke **stdout**. Ganti baris `echo "TODO"` dengan implementasimu. Jangan ubah format output.

Total nilai: **100 poin**

| Soal | Tingkat Kesulitan | Poin |
|------|------------------|------|
| 1 — Pemformat Nama | Mudah | 20 poin (4 × 5) |
| 2 — Pemeriksa Memori | Mudah-Sedang | 20 poin (4 × 5) |
| 3 — Pengklasifikasi File | Sedang | 28 poin (4 × 7) |
| 4 — Pelapor Disk | Sedang | 32 poin (4 × 8) |

---

## Soal 1 — Pemformat Nama (20 poin)

**File:** `problem1/formatter`

Baca nama lengkap (nama depan dan belakang) dari stdin. Keluarkan dalam format `NAMABELAKANG, NamaDepan` — nama belakang ALL CAPS, nama depan Title Case.

**Contoh:**
```
$ echo "budi santoso" | ./problem1/formatter
SANTOSO, Budi
```

**Petunjuk:**
- Gunakan pemisahan kata bash: `read -r first last`
- Gunakan ekspansi parameter: `${var^^}` (huruf besar semua), `${var^}` (kapital huruf pertama)

---

## Soal 2 — Pemeriksa Memori (20 poin, Mudah-Sedang)

**File:** `problem2/memory-checker`

Baca dua baris dari stdin: total RAM dalam MB dan RAM yang digunakan dalam MB. Keluarkan RAM bebas, persentase penggunaan, dan status berdasarkan penggunaan:
- `Normal` jika penggunaan di bawah 70%
- `Warning` jika penggunaan 70%–89%
- `Critical` jika penggunaan 90% atau lebih

**Contoh:**
```
$ printf "8000\n2000\n" | ./problem2/memory-checker
Free: 6000 MB
Usage: 25%
Status: Normal
```

**Petunjuk:**
- Gunakan `$(( total - used ))` untuk menghitung bebas
- Gunakan `$(( used * 100 / total ))` untuk menghitung persentase
- Gunakan `if (( usage >= 90 ))` untuk pengecekan status

> Skrip `generate-memory-data` tersedia di direktori `problem2/` untuk menghasilkan data memori nyata dari sistemmu. Cari tahu cara menjalankannya dan pipe outputnya ke dalam skripmu.

---

## Soal 3 — Pengklasifikasi File (28 poin, Sedang)

**File:** `problem3/file-classifier`

Baca daftar nama file dari stdin (satu per baris). Hitung berdasarkan jenisnya dan laporkan:
- Skrip shell yang berakhiran `.sh`
- File log yang berakhiran `.log`
- File konfigurasi yang berakhiran `.conf`
- Semua yang lain sebagai `Others`

**Contoh:**
```
$ printf "deploy.sh\nerror.log\nnginx.conf\nreadme.txt\n" | ./problem3/file-classifier
Scripts (.sh): 1
Logs (.log): 1
Configs (.conf): 1
Others: 1
```

**Petunjuk:**
- Gunakan loop `while IFS= read -r filename` untuk membaca setiap baris
- Gunakan pernyataan `case "$filename" in` dengan pola wildcard seperti `*.sh)`
- Gunakan `(( scripts++ ))` untuk menambah counter

> Skrip `generate-file-list` tersedia di direktori `problem3/` untuk membuat daftar file nyata dari sistemmu. Cari tahu cara menjalankannya dan pipe outputnya ke dalam skripmu.

---

## Soal 4 — Pelapor Disk (32 poin, Sedang)

**File:** `problem4/disk-reporter`

Baca baris dari stdin di mana setiap baris berisi nama pengguna dan penggunaan disk dalam MB (contoh: `alice 1200`). Laporkan:
- Total penggunaan disk semua pengguna
- Pengguna dengan penggunaan tertinggi (beserta ukurannya)
- Berapa banyak pengguna yang menggunakan lebih dari 1000 MB

**Contoh:**
```
$ printf "alice 1200\nbob 450\ncharlie 2800\n" | ./problem4/disk-reporter
Total usage: 4450 MB
Highest user: charlie (2800 MB)
Users over 1000 MB: 2
```

**Petunjuk:**
- Gunakan `read -r username size <<< "$line"` untuk memisahkan setiap baris menjadi dua variabel
- Gunakan `(( total += size ))` untuk mengakumulasi total
- Gunakan `if (( size > highest_size ))` untuk melacak pengguna dengan penggunaan tertinggi

> Skrip `generate-disk-usage` tersedia di direktori `problem4/` untuk mengumpulkan data penggunaan disk nyata dari sistemmu. Cari tahu cara menjalankannya dan pipe outputnya ke dalam skripmu.
