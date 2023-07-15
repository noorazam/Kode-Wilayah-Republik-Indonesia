# Kode Wilayah Republik Indonesia

adalah kode wilayah resmi yang ditentukan oleh kementerian dalam negeri RI melalui peraturan menteri dan/atau keputusan menteri. Kode dimulai dari 2 digit numerik kode propinsi, diikuti dengan 2 digit numerik kode kota/kabupaten, kemudian 2 digit numerik kode kecamatan, dan terakhir 4 digit numerik kode kelurahan/desa. Masing-masing tingkatan kode dipisahkan dengan titik (".").

### Kepmendagri no. 050-145 tahun 2022

Data mentah kepmendagri terakhir tentang _Pemberian dan Pemutakhiran Kode, Data Wilayah Administrasi Pemerintahan, dan Pulau Tahun 2021 adalah nomor 050-145 tahun 2022_ , berupa file pdf dan dipecah dalam 2 buah file: [`kepmendagri/kepmendagri.050-145.2022-aa`](kepmendagri/kepmendagri.050-145.2022-aa) dan [`kepmendagri/kepmendagri.050-145.2022-ab`](kepmendagri/kepmendagri.050-145.2022-ab). Untuk membaca, file ini harus digabungkan terlebih dahulu dengan cara:

    cat kepmendagri.050-145.2022* > kepmendagri.050-145.2022.pdf

### Data siap pakai

Data siap pakai dapat diambil di ['dist/csv/kodewilayah-2022-050.145.csv'](dist/csv/kodewilayah-2022-050.145.csv) berupa file _comma separated value_ dan ['dist/sql/kepmendagri-2022-050-145.sql'](dist/sql/kepmendagri-2022-050-145.sql) yang berupa data sql dan dapat langsung di_upload_ pada mesin MySQL atau MariaDB.

Pada data file CSV, kode wilayah masih mengikuti data mentah yang ada di kemendagri di atas, yaitu:
- kode provinsi hanya berisi 2 digit numerik; 
- kode kota/kabupaten berisi 2 digit kode provinsi dan 2 digit kode kota/kabupaten dipisahkan dengan titik ("."); 
- kode kecamatan berisi 2 digit kode provinsi, 2 digit kode kota/kabupaten, dan 2 digit kode kecamatan dengan dipisahkan dengan titi ("."); dan
- kode desa/kelurahan berisi 2 digit kode provinsi, 2 digit kode kota/kabupaten, 2 digit kode kecamatan, dan 4 digit kode desa/kelurahan dengan dipisahkan dengan titi (".").

Sementara pada SQL dilakukan penyesuaian dengan menambahkan ".00.00.0000" untuk kode provinsi, "00.0000" untuk kode kota/kabupaten, dan ".0000" untuk kode kecamatan. Hal ini diperlukan untuk memudahkan pencarian saat _query_ dilakukan. 
Sehingga saat mencari daftar propinsi, maka dapat dilakukan dengan melakukan query:

    SELECT * FROM `kodewil` WHERE kode_wil LIKE "%.00.00.0000";

Untuk mencari kota/kabupaten yang berada di wilayah provinsi Jawa Timur, maka dapat dilakukan query:

    SELECT * FROM `kodewil` WHERE kode_wil LIKE "35.%.00.0000";

Untuk mencari kecamatan yang berada di wilayah kota Surabaya, maka dapat dilakukan query:

    SELECT * FROM `kodewil` WHERE kode_wil LIKE "35.78.%.0000";

Dan untuk mencari desa/kelurahan yang berada di wilayah Gayungan kota Surabaya, maka dapat dilakukan query:

    SELECT * FROM `kodewil` WHERE kode_wil LIKE "35.78.22.%";
