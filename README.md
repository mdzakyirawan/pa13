# PROJECT AKHIR DDP Kel 13

# Gameshop
Sebuah sistem dimana admin dapat melakukan penjualan dan pengelolaan game serta pengguna dapat melakukan transaksi pembelian game

## Module & Library
1. `import os`: Digunakan untuk berinteraksi dengan sistem operasi.

2. `import json`: Digunakan untuk mengakses data JSON.

3. `import pwinput`: Digunakan untuk menampilkan **** untuk input kata sandi.

4. `from prettytable import PrettyTable`: Digunakan untuk membuat tabel rapi dalam teks.
```python
import os
import json 
import pwinput
from prettytable import PrettyTable
```

## Halaman User

Halaman untuk user setelah login program</br>

- Menyapa User sesuai dengan akun yang digunakan untuk login </br>
- Menampilkan Saldo user </br>
- Menampilkan Jumlah keranjang user

Menu
1. lihat game : mengarahkan user ke halaman untuk melihat game
2. Lihat isi keranjang : mengarahkan user ke halaman keranjang user 
3. Isi Saldo : mengarahkan user ke halaman untuk mengisi saldo user
4. Keluar : mengarahkan user ke halaman login

input untuk user memilih menu

![Screenshot 2023-11-01 061422](https://github.com/mdzakyirawan/pa13/assets/144348757/3fe94df1-17b7-4fff-b076-c525cc3df4d4)


## Halaman User Lihat Game
Halaman untuk user melihat daftar game</br>

Menampilkan daftar game menggunakan prettytable</br>
1. kembali ke menu : mengarahkan user ke menu user
2. beli game : mengarahkan user ke halaman pembelian game

input untuk pilihan user

![image](https://github.com/mdzakyirawan/pa13/assets/144348757/2bf6aef3-74dd-41ef-bd37-2de6efb453da)


## Halaman User Beli Game
Halaman untuk user dapat memilih game yang ingin dibeli</br>

Menampilkan daftar game yang tersedia</br>
input untuk user memilih game yang ingin dibeli 

![image](https://github.com/mdzakyirawan/pa13/assets/144348757/80bdff35-ddc7-4937-b3f0-4c50fae34281)


## Keranjang User
Keranjang untuk game game yang sudah dipilih oleh user</br>

Menampilkan tabel daftar game yang sudah ada di keranjang user

Pilihan aksi 
1. Hapus Barang : untuk menghapus game dari keranjang user
2. Checkout : untuk melakukan checkout dan transaksi pembelian game
3. Kembali ke menu : mengarahkan user kembali ke menu user

![image](https://github.com/mdzakyirawan/pa13/assets/144348757/4f8097ec-8153-4fa1-a8bd-fb4392e9436a)


## User Hapus Keranjang
Menampilkan tabel daftar game yang ada di keranjang user</br>
input untuk memilih game yang ingin dihapus user

![image](https://github.com/mdzakyirawan/pa13/assets/144348757/65148251-68e2-43a9-82db-c49fe63a3180)


## User Checkout
![image](https://github.com/mdzakyirawan/pa13/assets/144348757/93e2e069-125c-4c8e-9c61-80fada0adf89)



