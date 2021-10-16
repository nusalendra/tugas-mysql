1. (Menampilkan siapa karyawan yang pertama kali masuk) :  
SELECT * FROM karyawan WHERE tanggal_masuk =
(select tanggal_masuk from karyawan order by tanggal_masuk asc limit 1); 

2. Menampilkan total karyawan :  
SELECT COUNT(*) FROM karyawan;

3. Menampilkan daftar karyawan yang saat ini sedang cuti. Daftar berisi nomor_induk, nama, tanggal_mulai, lama_cuti dan keterangan.  
SELECT ck.nomor_induk, nama, tanggal_mulai, lama_cuti, keterangan 
FROM cuti_karyawan ck 
LEFT JOIN karyawan k 
ON ck.nomor_induk = k.nomor_induk;

4. Menampilkan daftar karyawan yang sudah cuti lebih dari satu kali. Daftar berisi no_induk, nama, jumlah (berapa kali cuti).  
SELECT ck.nomor_induk, nama, lama_cuti
FROM cuti_karyawan ck 
LEFT JOIN karyawan k 
ON ck.nomor_induk = k.nomor_induk
WHERE ck.lama_cuti > 1;

5.Menampilkan sisa cuti tiap karyawan tahun ini, jika di ketahui jatah cuti setiap karyawan tahun ini adalah 12. Daftar berisi no_induk, nama, sisa_cuti  
SELECT ck.nomor_induk, nama, (12 - lama_cuti) as sisa_cuti
FROM cuti_karyawan ck 
LEFT JOIN karyawan k 
ON ck.nomor_induk = k.nomor_induk;

6. Urutkan Data karyawan berdasakan nama, tampilkan Nomor_induk,nama,alamat,tanggal_lahir,lama_cuti  
SELECT k.nomor_induk, nama, alamat, tanggal_lahir, lama_cuti 
FROM cuti_karyawan ck 
LEFT JOIN karyawan k 
ON ck.nomor_induk = k.nomor_induk
ORDER BY k.nama asc;

7. Tentukan daftar gaji tiap tiap karyawan, jika gaji pokok 3jt dan dipotong cuti.. Data yang ditampilkan  No, No_induk, nama, gaji  
SELECT ck.nomor_induk, nama, (3000000 - (lama_cuti * 100000)) as gaji -- 100.000 didapat dari 3.000.000 / 30 hari --
FROM cuti_karyawan ck 
LEFT JOIN karyawan k 
ON ck.nomor_induk = k.nomor_induk;

8. tampilkan data karyawan yang cuti nya lebih dari 2 hari , data yang ditampilkan adalah No,Nomor_induk,nama, alamat, tanggal lahir, cuti  
SELECT ck.id, k.nomor_induk, nama, alamat, tanggal_lahir, lama_cuti 
FROM cuti_karyawan ck 
LEFT JOIN karyawan k 
ON ck.nomor_induk = k.nomor_induk
WHERE ck.lama_cuti > 2;

9. tampilkan karyawan yang cuti nya berhubungan dengan keperluan anaknya, data yang ditampilkan adalah No,Nomor_induk,nama, alamat, tanggal lahir, cuti, keterangan  
SELECT id, ck.nomor_induk, nama, alamat, tanggal_lahir, lama_cuti, keterangan  
FROM cuti_karyawan ck  
LEFT JOIN karyawan k   
ON ck.nomor_induk = k.nomor_induk  
WHERE keterangan LIKE "%anak%";

10. tampilkan umur tiap2 karyawan, jika pesangon tiap tahun nya 3jt, data yang ditampilkan No, Nomor_induk, Nama, Alamat, tanggal_lahir, umur, pesangon  
SELECT nomor_induk, nama, alamat, YEAR (CURDATE()) - YEAR (tanggal_lahir) as umur  
FROM karyawan k;
