## API Sistem Pengecekan Jadwal Kuliah Universitas Budiluhur

Application Programming Interface untuk mengambil data
Jadwal harian perkuliahan dari semua fakultas di Kampus `Universitas Budiluhur Jakarta`.

### Required Package
package-package yang dibutuhkan ada di dalam file `requirements.txt`. berupa :
```
requests==2.8.1
beautifulsoup4==4.4.1
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
### Dapatkan Data Fakultas
untuk mendapatkan semua data fakultas
```python
from budiluhur.jadwal import fakultas

# inisialisasi class Fakultas
f = fakultas.Fakultas()
fakultas_all = f.get_all()
print(fakultas_all)
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

### Daptkan Data Fakultas Dengan ID
untuk mendapatkan hanya satu data fakultas kita perlu untuk mendapatkan kode fakultas
#### Dapatkan Kode Fakultas
##### TODO
