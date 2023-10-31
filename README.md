# PROJECT AKHIR DDP Kel 13

# Gameshop
Sebuah sistem dimana admin dapat melakukan penjualan dan pengguna dapat melakukan transaksi pembelian game

## Module & Library
1. `import os`: Digunakan untuk berinteraksi dengan sistem operasi.

2. `import json`: Digunakan untuk mengkodekan dan mendekode data JSON.

3. `import pwinput`: Digunakan untuk menampilkan **** untuk input kata sandi.

4. `from prettytable import PrettyTable`: Digunakan untuk membuat tabel rapi dalam teks.
```python
import os
import json 
import pwinput
from prettytable import PrettyTable
```

## Halaman User

Halaman untuk user setelah login program 

```python
def user(nama_user): 
    print(f"Hai, {nama_user}")

    print("Saldo Wallet : ")
    print("Keranjang ()\n")
    
    print("Menu")
    print("1. Lihat Game")
    print("2. Lihat isi Keranjang")
    print("3. Isi Saldo")
    print("4. Keluar\n")
    input_halaman_user = input("Pilih menu : ")

    if input_halaman_user == "1" :
        user_lihat_game(nama_user)
    elif input_halaman_user == "2":
        user_keranjang(nama_user)
    elif input_halaman_user == "3":
        user_isi_saldo(nama_user)
    elif input_halaman_user == "4":
        login()
```
![Screenshot 2023-11-01 061422](https://github.com/mdzakyirawan/pa13/assets/144348757/59ee8cb5-c675-409f-ac70-d599156719b0)


## Halaman User Lihat Game
Halaman untuk user dapat melihat daftar game yang tersedia
```python
def user_lihat_game(nama_user):
    clear_screen()
    tabel_game = PrettyTable()
    tabel_game.field_names = ['ID','Nama Game', 'Developer', 'Tahun Rilis', 'Versi Game', 'Harga Game']

    for item in data_game2['game']:
        tabel_game.add_row([item['ID'],item['nama_game'], item['developer'], item['tahun_rilis'], item['versi_game'], item['harga_game']])

    print(tabel_game)

    print("1. kembali ke menu")
    print("2. beli game\n")

    lihat_game = input("Pilih : ")

    if lihat_game == "1":
        user(nama_user)
    elif lihat_game == "2":
        user_beli_game(nama_user)
    else:
        print("pilihan tidak valid")
```
![image](https://github.com/mdzakyirawan/pa13/assets/144348757/bfaabb52-9b3a-40ad-948d-325c6a637f02)

## Halaman User Beli Game
Halaman untuk user dapat memilih game yang ingin dibeli

```python
def user_beli_game(nama_user):
    tabel_game = PrettyTable()
    tabel_game.field_names = ['ID','Nama Game', 'Developer', 'Tahun Rilis', 'Versi Game', 'Harga Game']

    for item in data_game2['game']:
        tabel_game.add_row([item['ID'],item['nama_game'], item['developer'], item['tahun_rilis'], item['versi_game'], item['harga_game']])
    print(tabel_game)
    
    id_produk = input("Masukkan ID produk yang akan dibeli (0 untuk selesai): ")
    game_co = None

    for game in data_game2['game']:
        if game["ID"] == id_produk:
            game_co = game
    
    if game_co != None:
        print()
    else:
        print('Data Tidak Ada')

    nama_game_co = str(game_co['nama_game'])
    harga_game_co = int(game_co['harga_game'])

    co_keranjang = {
        "nama_game" : nama_game_co,
        "harga_game" : harga_game_co,
        "nama_user" : nama_user
    }

    if "keranjang" not in data_keranjang2:
        data_keranjang2["keranjang"] = []

    data_keranjang2["keranjang"].append(co_keranjang)

    with open(path_keranjang2, 'w') as file:
        json.dump(data_keranjang2, file, indent=4)

    print('Barang Berhasil Ditambahkan ke Keranjang')
```

## Keranjang User
Keranjang untuk game game yang sudah dipilih oleh user
```python
def user_keranjang(nama_user):
    tabel_keranjang = PrettyTable()
    tabel_keranjang.field_names = ['Nama Game', 'Harga Game']

    keranjang_user = []
    for x in data_keranjang2['keranjang']:
        if x['nama_user'] == nama_user:
            keranjang_user.append(x)

    for x in keranjang_user:
        tabel_keranjang.add_row([x['nama_game'], x['harga_game']])

    if not keranjang_user:
        print("Keranjang Anda kosong.")
    else:
        print("Isi Keranjang Anda : ")
        print(tabel_keranjang)
        print('Pilih Aksi yang ingin Anda Lakukan')
        print('1. Hapus Barang Yang Ada Di Keranjang')
        print('2. Checkout Barang Di Keranjang')
        print('3. Kembali Ke Menu')
        aksi_keranjang = input('Masukkan Pilihan : ')

        if aksi_keranjang == '1':
            hapus_keranjang(nama_user)
        elif aksi_keranjang == '2':
            user_checkout(nama_user)
        elif aksi_keranjang == '3':
            user(nama_user)
```

## User Hapus Keranjang
```python
def hapus_keranjang(nama_user):
    clear_screen()
    tabel_keranjang = PrettyTable()
    tabel_keranjang.field_names = ['No', 'Nama Game', 'Harga Game']

    keranjang_user = []
    for x in data_keranjang2['keranjang']:
        if x['nama_user'] == nama_user:
            keranjang_user.append(x)

    nomor_urutan = 1
    for x in keranjang_user:
        tabel_keranjang.add_row([nomor_urutan, x['nama_game'], x['harga_game']])
        nomor_urutan += 1

    print(tabel_keranjang)
    pilihan = int(input('Hapus barang yang dipilih : '))
    index_barang = pilihan - 1
    game_hapus = keranjang_user[index_barang]['nama_game']

    for item in data_keranjang2['keranjang']:
        if item['nama_user'] == nama_user and item['nama_game'] == game_hapus:
            data_keranjang2['keranjang'].remove(item)
    
    with open(path_keranjang2, 'w') as file:
        json.dump(data_keranjang2, file, indent=4)
    
    print('Data Berhasil Dihapus')
    user_keranjang(nama_user)
```

## User Checkout
```python
def user_checkout(nama_user):
    total_harga = 0
    
    clear_screen()
    print('Anda Ingin Membeli :')
    for x in data_keranjang2['keranjang']:
        if x['nama_user'] == nama_user:
            game_co = x['nama_game']
            harga_co = x['harga_game']
            total_harga += harga_co
            print(game_co)
    print(f'Seharga {total_harga}')

    for y in data_user2['users']:
        if y['username'] == nama_user:
            saldo_user = y['saldo_wallet']

    transaksi = False

    if total_harga >= saldo_user:
        print('Saldo Anda Tidak Cukup')
        print('1. Top Up Saldo')
        print('2. Batalkan Transaksi')
        pilihan = input('Masukkan Pilihan Anda : ')
        if pilihan == '1':
            user_isi_saldo(nama_user)
        elif pilihan == '2':
            print('Transaksi Dibatalkan')
        
    elif total_harga <= saldo_user:
        print('Saldo Anda Cukup')
        print('1. Konfirmasi Pembayaran')
        print('2. Top Up Saldo')
        print('3. Batalkan Transaksi')
        pilihan = input('Masukkan Pilihan Anda : ')
        if pilihan == '1':
            print('Lanjutkan Pembayaran')
            transaksi = True
        elif pilihan == '2':
            user_isi_saldo(nama_user)
        elif pilihan == '3':
            print('Transaksi Dibatalkan')

    if transaksi == True:
        clear_screen()
        print(f'Total pembayaran Anda : Rp. {total_harga}')
        print(f'Saldo Anda            : Rp. {saldo_user}')

        konfirmasi_pin = int(input('Masukkan Pin Anda : '))
        for x in data_user2['users']:
            if x['username'] == nama_user:
                if x['pin_wallet'] == konfirmasi_pin:
                    sisa_saldo = saldo_user-total_harga
                    print('Pin Terkonfirmasi, Pembayaran Berhasil')
                else:
                    print('Pin Salah')

        for item in data_keranjang2['keranjang']:
            if item['nama_user'] == nama_user:
                data_riwayat2['riwayat'].append({"nama_game": item["nama_game"], "pembeli": nama_user})

        data_keranjang2['keranjang'] = [item for item in data_keranjang2['keranjang'] if item['nama_user'] != nama_user]

        for x in data_user2['users']:
            if x['username'] == nama_user:
                x['saldo_wallet'] = sisa_saldo

    with open(path_user2, 'w') as file:
        json.dump(data_user2, file, indent=4)

    with open(path_keranjang2, 'w') as file:
        json.dump(data_keranjang2, file, indent=4)
    
    with open(path_riwayat2, 'w') as file:
        json.dump(data_riwayat2, file, indent=4)
```

