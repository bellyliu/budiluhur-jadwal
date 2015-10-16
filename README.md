## API Sistem Pengecekan Jadwal Kuliah Universitas Budiluhur

Application Programming Interface untuk mengambil data
Jadwal harian perkuliahan dari semua fakultas di Kampus `Universitas Budiluhur Jakarta`.

### Instalasi
untuk menginstall package `budiluhur-jadwal` melalui `pip`, ketik di terminal
```
$ pip install budiluhur-jadwal
```

### Required Package
package-package yang dibutuhkan ada di dalam file `requirements.txt`. berupa :
```
requests==2.8.1
beautifulsoup4==4.4.1
python-Levenshtein
```
untuk instalasi semua package yang dibutuhkan adalah
```
$ pip install -r requirements.txt
```

### Fakultas
inisialisasi kelas `Fakultas` yang di import dari package `budiluhur.jadwal.fakultas.Fakultas`.

```python
from budiluhur.jadwal import fakultas

# inisialisasi class Fakultas
f = fakultas.Fakultas()
```
### dapatkan semua data fakultas
untuk mendapatkan semua data fakultas
```python
from budiluhur.jadwal import fakultas

# inisialisasi class Fakultas
f = fakultas.Fakultas()
fakultas_bl = f.get_all()
print(fakultas_bl)
```
hasil yang diperoleh
```
{'01': 'Fakultas Teknologi Informasi',
 '02': 'Akademi Sekretari',
 '03': 'Fakultas Ekonomi',
 '04': 'Fakultas Ilmu Sosial Dan Ilmu Politik',
 '05': 'Fakultas Teknik',
 '07': 'Fakultas Ilmu Komunikasi',
 '33': 'Fakultas D3 Unggulan'}
```

### dapatkan data fakultas dengan ID
untuk mendapatkan hanya satu data fakultas kita perlu untuk mendapatkan kode fakultas. sebelumnya
kita sudah memperolah dict fakultas, asumsikan kita akan mengambil nilai fakultas `Akademi Sekretari`,
maka kodenya :
```python
f = fakultas.Fakultas()
akademi_sekretari = f.get_fakultas(kode_fakultas='02')
print(akademi_sekretari)
```
Hasilnya
```
{'02': 'Akademi Sekretari'}
```

### ambil jadwal berdasarkan fakultas yang dipilih
dari fakultas, kita bisa mendapatkan semua list jadwal dosen pengajar pada waktu dan tanggal saat ini.
```python
from budiluhur.jadwal import fakultas
from pprint import pprint

# inisialisasi class Fakultas
fak = fakultas.Fakultas()
fti = fak.get_fakultas('01', True)
print(fti.jadwal.get_all())
```
hasil yang diperoleh adalah semua jadwal berdasarkan fakultas yang dipilih.
```
[{'Kel': 'KU',
  'Keterangan': 'Masuk',
  'Matakuliah': 'Wawasan Budi Luhur',
  'Mulai': '18:10',
  'Nama Dosen': 'ALI MUHAMMAD',
  'No.': '1.',
  'Ruang': '6.2.5',
  'Selesai': '21:40'},
 {'Kel': 'KU',
  'Keterangan': 'Masuk',
  'Matakuliah': 'Pemeliharaan Perangkat Lunak',
  'Mulai': '18:10',
  'Nama Dosen': 'ARSANTO NARENDRO',
  'No.': '2.',
  'Ruang': '8.3.A',
  'Selesai': '21:40'},
 {'Kel': 'KU',
  'Keterangan': 'Pengganti',
  'Matakuliah': 'ASP .NET',
  'Mulai': '18:10',
  'Nama Dosen': 'ATIK ARIESTA',
  'No.': '3.',
  'Ruang': 'L.A.B',
  'Selesai': '21:40'},
 {'Kel': 'KU',
  'Keterangan': 'Masuk',
  'Matakuliah': 'Statistik Ekonomi',
  'Mulai': '18:10',
  'Nama Dosen': 'DJATI KUSDIARTO',
  'No.': '4.',
  'Ruang': '8.3.5',
  'Selesai': '21:40'},
.............. ]
```
### memfilter kehadiran
kita juga bisa memfilter jadwal sesuai dengan status kehadiran dosen di kelas.
disini kita menggunakan method `filter_kehadiran` dimana `method` ini secara default
menampilkan list jadwal dosen yang tidak hadir.
```python
from budiluhur.jadwal import fakultas
from pprint import pprint

# inisialisasi class Fakultas
fak = fakultas.Fakultas()
# id fakultas bisa diperoleh di fak.get_all()
fe = fak.get_fakultas('03', True) # Fakultas Ekonomi
print(fe.jadwal.filter_kehadiran())
```
Hasil yang diperoleh
```
[{'Kel': 'BU',
  'Keterangan': 'Tidak Hadir',
  'Matakuliah': 'Pendidikan Agama Islam',
  'Mulai': '18:10',
  'Nama Dosen': 'YANTI FITRIANI',
  'No.': '13.',
  'Ruang': '4.2.4',
  'Selesai': '21:40'}]
```
untuk mengecek hanya dosen yang hadir dalam jadwal tertentu, kita bisa menambahkan
nilai parameter untuk method `filter_kehadiran` menjadi `'masuk'`:
```python
...
fe = fak.get_fakultas('03', True) # Fakultas Ekonomi
print(fe.jadwal.filter_kehadiran('masuk'))
```
hasilnya berupa
```
[{'Kel': 'BV',
  'Keterangan': 'Masuk',
  'Matakuliah': 'Pengantar Akuntansi/Lab',
  'Mulai': '18:10',
  'Nama Dosen': 'AGUS TRIYONO',
  'No.': '1.',
  'Ruang': '6.3.2',
  'Selesai': '21:40'},
 {'Kel': 'BU',
  'Keterangan': 'Masuk',
  'Matakuliah': 'Pengantar Akuntansi/Lab',
  'Mulai': '18:10',
  'Nama Dosen': 'DICKY ARISUDHANA',
  'No.': '3.',
  'Ruang': '6.3.1',
  'Selesai': '21:40'},
......]
```
untuk mengecek hanya dosen yang hadir dalam jadwal tertentu, kita bisa mengubah
nilai parameter method `filter_kehadiran` menjadi:
```python
fe = fak.get_fakultas('03', True) # Fakultas Ekonomi
print(fe.jadwal.filter_kehadiran('pengganti'))
```
> parameter pun bisa menjadi `izin`.

### mendapatkan data jadwal dari nama dosen
kita juga bisa mendapatkan jadwal dari nama dosen yang terkait dengan method
`get_from_dosen` dengan parameter `nama_dosen` berupa string dari nama dosen.
```python
from budiluhur.jadwal import fakultas
from pprint import pprint

# inisialisasi class Fakultas
fak = fakultas.Fakultas()
# id fakultas bisa diperoleh di fak.get_all()
fe = fak.get_fakultas('03', True) # Fakultas Ekonomi
pprint(fe.jadwal.get_from_dosen('agus triyono'))
```
diperoleh hasil berupa
```
[{'Kel': 'BV',
  'Keterangan': 'Masuk',
  'Matakuliah': 'Pengantar Akuntansi/Lab',
  'Mulai': '18:10',
  'Nama Dosen': 'AGUS TRIYONO',
  'No.': '1.',
  'Ruang': '6.3.2',
  'Selesai': '21:40'}]
```

### mendapatkan data jadwal dari kelas atau ruangan
kita juga bisa mendapatkan jadwal dari nama ruangannya.
```python
from budiluhur.jadwal import fakultas
from pprint import pprint

# inisialisasi class Fakultas
fak = fakultas.Fakultas()
# id fakultas bisa diperoleh di fak.get_all()
fe = fak.get_fakultas('03', True) # Fakultas Ekonomi
pprint(fe.jadwal.get_from_ruangan('4.3.3'))
```
hasil berupa
```
[{'Kel': 'BU',
  'Keterangan': 'Pengganti',
  'Matakuliah': 'Aspek Hukum Dalam Bisnis',
  'Mulai': '18:10',
  'Nama Dosen': 'ASTRID DITA MEIRINA HAKIM',
  'No.': '2.',
  'Ruang': '4.3.3',
  'Selesai': '21:40'}]
```

## Thanks To
> All My Friends In Kabel Konslet, Morpyn Behind The Canteen, I love u all.

## MIT License
> #### Copyright (c) 2015 Yanwar Solahudin

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

> The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

> THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
