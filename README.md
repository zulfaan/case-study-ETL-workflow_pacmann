# ETL Pipeline dengan Luigi

## Deskripsi Tugas
Proyek ini menunjukkan bagaimana membangun pipeline ETL menggunakan **Luigi**. Pipeline ini akan menangani ekstraksi, validasi, transformasi, dan pemuatan data (ETL) untuk kasus analisis hotel.

### Desain Pipeline ETL yang Diusulkan
Pipeline ETL ini melibatkan beberapa tahap: ekstraksi, validasi, transformasi, dan pemuatan. Desain pipeline adalah sebagai berikut:

### Pembagian Tugas

1. **Ekstraksi Data:**
   - **Sumber Data:**
     - API: [Data Payment](https://shandytepe.github.io/payment.json)
     - Database: Data Hotel
   - **Tindakan:** Ekstrak data dari sumber-sumber tersebut dan simpan output sebagai file `.csv` di folder `data_extract`.

2. **Validasi Data:**
   - **Tugas Validasi:**
     - Periksa bentuk data
     - Periksa tipe data kolom
     - Periksa nilai yang hilang (missing values)
   - **Tindakan:** Validasi data yang diekstrak dan laporkan jika ada ketidaksesuaian.

3. **Transformasi Data:**
   - **Tugas Transformasi:**
     - Gabungkan data dari beberapa sumber menjadi satu tabel yang bersih:
       - `payment` (Data Pembayaran API)
       - `reservation` (DB Hotel)
       - `customer` (DB Hotel)
   - **Tindakan:** Lakukan transformasi yang diperlukan, seperti penggabungan, penambahan kolom baru, dan penanganan nilai yang hilang atau salah.
   - Setelah transformasi berhasil, simpan data hasilnya sebagai file `.csv` di folder `data_transform`.

4. **Memuat Data ke Data Warehouse:**
   - **Tindakan:** Muat data yang telah ditransformasikan ke dalam Data Warehouse.

5. **Menggabungkan Semua Pipeline:**
   - **Tindakan:** Gunakan **Luigi** untuk mengorkestrasi dan menggabungkan ekstraksi, validasi, transformasi, dan pemuatan data ke dalam satu pipeline yang terintegrasi.

6. **Menjadwalkan Pipeline:**
   - **Tindakan:** Jadwalkan pipeline untuk berjalan setiap 2 menit menggunakan **cron**. Ekspresi cron untuk jadwal ini adalah:
     ```bash
     */2 * * * * /path/to/pipeline.sh
     ```

7. **Proses UPSERT:**
   - **Tindakan:** Implementasikan fungsi UPSERT untuk memastikan bahwa data diperbarui dengan benar di Data Warehouse, menguji kekuatan pipeline yang telah dibuat.

## Prasyarat
- Python 3.7+
- Libraries:
  - **Luigi**
  - **Pandas**
  - **SQLAlchemy**
  - **psycopg2**
- Instansi PostgreSQL yang berjalan untuk Data Warehouse.

## Instruksi Pengaturan
1. **Instal dependensi yang diperlukan:**
   ```bash
   pip install luigi pandas sqlalchemy psycopg2