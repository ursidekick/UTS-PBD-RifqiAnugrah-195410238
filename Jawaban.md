# UTS-PBD-RifqiAnugrah-195410238
UTS Pengenalan Big Data - Rifqi Anugrah (195410238)

Nomor 1
Cari dan sebutkan 3 DBMS yang bisa digunakan untuk mengelola big data
Jawaban :

OODBMS
1.Database berorientasi objek Versant 
2.ObjectDB
3.ObjectStore

RDBMS
1.Microsoft Access
2.MySQL
3.Microsoft SQL Server

ORDBMS
1.Microsoft SQL ServerOracle Database
2.PostgreSQL
3.Oracle DB



Nomor 2
Carilah contoh masalah big data yang bisa dikelola menggunakan salah satu DBMS tersebut, jelaskan mulai dari instalasi sampai CRUD 
untuk data menggunakan DBMS tersebut. Asumsikan anda akan memecahkan masalah big data yang sudah anda cari contoh tadi, 
jelaskan kira-kira bagaimana arsitektur dari solusi big data menggunakan DBMS tersebut, gambarkan diagramnya.
Jawaban :

Penyelesaian Masalah Terkait Extract, Transform, dan Load Data Dengan MySQL
(Saya menggunakan beberapa komponen dari mata kuliah Big Data Analytic sebagai sample untuk memudahkan proses penjelasan).

1.	Langkah pertama yang dilakukan adalah masuk ke dalam folder instalasi python pada PC atau laptop kita masing-masing.

2.	Selanjutnya instal library atau modul pandas, xlrd, sqlalchemy dan pymysql pada python kita masing-masing.]

3.	Pastikan instalasi berhasil dilakukan dengan mengetikkan perintah “python”. Kemudian dilanjutkan dengan mengetikkan masing-masing 
perintah import pandas, xlrd, sqlalchemy dan pymysql. Jika tidak terdapat pesan error maka instalasi yang telah dilakukan bisa dinyatakan
sepenuhnya berhasil.

4.  Siapkan file yang akan kita olah seperti file pegawai_cab01.csv dan pegawai_cab01.csv (ini saya menggunakan file dari materi Big Data Analytic sebagai sample)

5.	Berikutnya kita harus membuat satu database dengan nama bigdata6. Disini saya menggunakan phpMyAdmin untuk pengaturan databasenya.

6.  Skenario untuk praktik ini: terdapat 2 buah dokumen dengan jenis berbeda yaitu pegawai_cab01.csv berupa file CSV dan pegawai_cab02.xlsx berupa file Excell. 
Data pegawai_cab01.csv terdiri dari: nik, nama, gaji, tglmasuk, job_id, job_title, sedangkan file pegawai_cab02.xlsx terdiri dari : nik, nama, job,status. 
Status berisi tulisan “OUT” jika pegawai tersebut sudah keluar. Goalnya adalah, menggabungkan isi file pegawai_cab01.csv dan pegawai_cab02.xlsx untuk field nik,
nama, job_id ke tabel pegawai, sedangkan job_id dan job_title akan masuk ke tabel Job.

7.	Membuat sebuah file python dan mengetikkan kode seperti gambar dibawah ini:
import pandas as pd
df_csv = pd.read_csv("pegawai_cab01.csv")
print(df_csv)

hasilnya akan seperti ini :
     nik             nama     gaji    tglmasuk      job_id  \
0    206    William Gietz   8300.0  1990-10-01  AC_ACCOUNT   
1    205  Shelley Higgins  12000.0  1987-09-30      AC_MGR   
2    200  Jennifer Whalen   4400.0  1987-09-25     AD_ASST   
3    100      Steven King  24000.0  1983-06-17     AD_PRES   
4    101    Neena Kochhar  17000.0  1987-06-18       AD_VP   
..   ...              ...      ...         ...         ...   
102  120    Matthew Weiss   8000.0  1984-07-07      ST_MAN   
103  121       Adam Fripp   8200.0  1984-07-08      ST_MAN   
104  122   Payam Kaufling   7900.0  1987-07-09      ST_MAN   
105  123   Shanta Vollman   6500.0  1987-07-10      ST_MAN   
106  124    Kevin Mourgos   5800.0  1987-07-11      ST_MAN   

                         job_title  
0                Public Accountant  
1               Accounting Manager  
2         Administration Assistant  
3                        President  
4    Administration Vice President  
..                             ...  
102                  Stock Manager  
103                  Stock Manager  
104                  Stock Manager  
105                  Stock Manager  
106                  Stock Manager  

[107 rows x 6 columns]

8. 	Kode dibawah ini digunakan untuk menampilkan data nik, nama dan job_id dari file pegawai_cab01.csv.
import pandas as pd
df_csv = pd.read_csv("pegawai_cab01.csv")
df_csv_filter = df_csv[['nik','nama','job_id']]
print(df_csv_filter)

hasilnya akan seperti ini:
     nik             nama      job_id
0    206    William Gietz  AC_ACCOUNT
1    205  Shelley Higgins      AC_MGR
2    200  Jennifer Whalen     AD_ASST
3    100      Steven King     AD_PRES
4    101    Neena Kochhar       AD_VP
..   ...              ...         ...
102  120    Matthew Weiss      ST_MAN
103  121       Adam Fripp      ST_MAN
104  122   Payam Kaufling      ST_MAN
105  123   Shanta Vollman      ST_MAN
106  124    Kevin Mourgos      ST_MAN

[107 rows x 3 columns]

9.	Langkah berikutnya adalah untuk membaca file pegawai_cab01.xlsx menggunakan kode dibawah ini.
import pandas as pd
df_excel = pd.read_excel("pegawai_cab02.xlsx")
print(df_excel)

hasilnya akan seperti ini:
   nik  nama      job status
0  403  Rina   SA_REP    NaN
1  404  Toro  IT_SUPP    NaN
2  405  Siti   SA_REP    OUT
3  406  Rini   SA_REP    NaN


10.	Memodifikasi kode sebelumnya agar data yang terambil hanya yang status bukan OUT, kemudian kolom yang dibutuhkan disamakan 
dengan pegawai_cab01 yaitu nik, nama dan job.
import pandas as pd
df_excel = pd.read_excel("pegawai_cab02.xlsx")
df_excel_filter = df_excel[df_excel['status'] != 'OUT']
df_excel_filter = df_excel_filter[['nik','nama','job'] ]
print(df_excel_filter)

hasilnya akan seperti ini:
   nik  nama      job
0  403  Rina   SA_REP
1  404  Toro  IT_SUPP
3  406  Rini   SA_REP

11.	Karena kedua hasil tersebut akan digabung maka nama kolom harus sama. Lalu langkah selanjutnya adalah memodifikasi nama kolom
“job” menjadi “job_id”.
import pandas as pd
df_excel = pd.read_excel("pegawai_cab02.xlsx")
df_excel_filter = df_excel[df_excel['status'] != 'OUT']
df_excel_filter = df_excel_filter[['nik','nama','job'] ]
df_excel_filter = df_excel_filter.rename(columns={'job':'job_id'})
print(df_excel_filter)

hasilnya akan seperti ini:
   nik  nama   job_id
0  403  Rina   SA_REP
1  404  Toro  IT_SUPP
3  406  Rini   SA_REP

12.	Menggabungkan isi file.
import pandas as pd
df_csv = pd.read_csv("pegawai_cab01.csv")
df_csv_filter = df_csv[['nik','nama','job_id']]
df_excel = pd.read_excel("pegawai_cab02.xlsx")
df_excel_filter = df_excel[df_excel['status'] != 'OUT']
df_excel_filter = df_excel_filter[['nik','nama','job'] ]
df_excel_filter = df_excel_filter.rename(columns={'job':'job_id'})
df_gabung = df_csv_filter.append(df_excel_filter)
print(df_gabung)

hasilnya akan seperti ini:
     nik             nama      job_id
0    206    William Gietz  AC_ACCOUNT
1    205  Shelley Higgins      AC_MGR
2    200  Jennifer Whalen     AD_ASST
3    100      Steven King     AD_PRES
4    101    Neena Kochhar       AD_VP
..   ...              ...         ...
105  123   Shanta Vollman      ST_MAN
106  124    Kevin Mourgos      ST_MAN
0    403             Rina      SA_REP
1    404             Toro     IT_SUPP
3    406             Rini      SA_REP

[110 rows x 3 columns]

13.	Berikutnya adalah mengkoneksikan ke database MySQL lalu ketikkan kode seperti gambar dibawah ini.
import sqlalchemy as sql
conn_string = "mysql+pymysql://root:@localhost/bigdata6"
sql_engine = sql.create_engine(conn_string)
res = sql_engine.execute("show databases")
for r in res:
    print(r[0])
    
 hasilnya akan seperti ini:
 bigdata6
information_schema
mysql
performance_schema
phpmyadmin
test
toko
toko_electronik

14.	Modifikasi kode sebelumnya dengan menambahkan import pandas pada paris ke-2. Df_gabung.to_sql menunjukkan bahwa data di dataframe
df_gabung, disimpan ke tabel bernama pegawai, menggunakan koneksi sql_engine. Jika sudah ada maka akan ditimpa, serta tidak menyertakan
index dari dataframe ini.
import sqlalchemy as sql
import pandas as pd
conn_string = "mysql+pymysql://root:@localhost/bigdata6"
sql_engine = sql.create_engine(conn_string)
df_csv = pd.read_csv("pegawai_cab01.csv")
df_csv_filter = df_csv[['nik','nama','job_id']]
df_excel = pd.read_excel("pegawai_cab02.xlsx")
df_excel_filter = df_excel[df_excel['status'] != 'OUT']
df_excel_filter = df_excel_filter[['nik','nama','job'] ]
df_excel_filter = df_excel_filter.rename(columns={'job':'job_id'})
df_gabung = df_csv_filter.append(df_excel_filter, "index=False")
df_gabung.to_sql("pegawai",con=sql_engine,
                if_exists='replace',index=False)
print("Load ke MySQL selesai")

hasilnya akan seperti ini
Load ke MySQL selesai

15.	Langkah terakhir adalah Load data Job dengan mengetikkan kode dibawah ini.
import sqlalchemy as sql
import pandas as pd
conn_string = "mysql+pymysql://root:@localhost/bigdata6"
sql_engine = sql.create_engine(conn_string)
ds = pd.read_csv("pegawai_cab01.csv")
df = ds[['job_id','job_title']].drop_duplicates()
df.to_sql("job", con=sql_engine, if_exists='replace',index=False)

hasilnya akan berupa penambahan tabel pada MySQL masing-masing pengguna
