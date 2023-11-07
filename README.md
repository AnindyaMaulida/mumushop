1. Apa perbedaan utama antara stateless dan stateful widget dalam konteks pengembangan aplikasi Flutter?
Stateless widget adalah widget yang tidak berubah dan tidak memiliki state. Stateless widget dirender sekali dan tidak diperbarui kecuali ada perubahan data eksternal. Contohnya termasuk Text, Icon, dan RaisedButton.

Stateful widget adalah widget yang dapat berubah dan memiliki state yang. Stateful widget dapat memperbarui properti atau state mereka selama masa hidup widget, menggambarnya ulang beberapa kali, dan merespons interaksi pengguna atau data eksternal. Contoh stateful widget meliputi Checkbox, Radio Button, Slider, InkWell, Form, dan TextField.

Dalam penggunaan nya stateless widget lebih sederhana, mudah digunakan, dan mudah dipelihara, tetapi memiliki keterbatasan dalam fungsionalitas dan interaktivitas. Sedangkan stateful widget lebih kompleks, memerlukan lebih banyak kode, namun memberikan fleksibilitas dan kontrol yang lebih besar terhadap perilaku dan penampilan widget.

2. Sebutkan seluruh widget yang kamu gunakan untuk menyelesaikan tugas ini dan jelaskan fungsinya masing-masing.
    - MyApp: Widget ini berisi kelas yang mewarisi StatelessWidget dan berfungsi sebagai titik masuk aplikasi yang memuat MyHomePage.
    - MyHomePage: Widget ini berisi kelas yang mewarisi StatelessWidget dan merupakan halaman utama aplikasi. Ini berisi Scaffold yang memuat AppBar, SingleChildScrollView, dan daftar item toko.
    - Scaffold: Widget ini menyediakan kerangka dasar untuk halaman dengan AppBar dan body.
    - AppBar: Widget ini menampilkan AppBar di bagian atas halaman dengan judul "Mumu Shop" yang menggunakan Text untuk menampilkan teks.
    - SingleChildScrollView: Widget ini merupakan widget pembungkus yang memungkinkan kontennya untuk bisa discroll jika lebih besar dari layar.
    - Padding:  Widget ini digunakan untuk memberikan padding ke kontennya.
    - Column:  Widget ini digunakan untuk menampilkan komponen secara vertikal dalam daftar.
    - GridView.count:  Widget ini digunakan untuk menampilkan daftar item toko dalam grid dengan jumlah kolom yang telah ditentukan.
    - ShopItem: Widget ini berisi kelas yang mendefinisikan item toko dengan nama dan ikonnya.
    - ShopCard: Widget ini berisi kelas yang mewarisi StatelessWidget dan digunakan untuk menampilkan setiap item toko. Ini berisi Material, InkWell, Container, Icon, dan Text untuk menampilkan kontennya.
    - Color, TextAlign, TextStyle: Widget ini digunakan untuk mengatur warna, penataan teks, dan gaya teks yang diterapkan pada teks dalam aplikasi.
    - SnackBar: Widget ini digunakan untuk menampilkan pesan pemberitahuan ketika item toko diklik.

3. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial)
    1. pertama saya mmbuat app bernama mumuashop dengan menjalankan 
    ``` flutter create mumushop```
    2. selanjutnya saya membuat file bernama menu.dart dan menambahkan kode berikut
    ```dart
    import 'package:flutter/material.dart';

    void main() {
    runApp(MyApp());
    }

    class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
        return MaterialApp(
        home: MyHomePage(),
        );
    }
    }

    class MyHomePage extends StatelessWidget {
    MyHomePage({Key? key}) : super(key: key);

    final List<ShopItem> items = [
        ShopItem("Lihat Item", Icons.checklist),
        ShopItem("Tambah Item", Icons.add_shopping_cart),
        ShopItem("Logout", Icons.logout),
    ];

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: Text(
            'Mumu Shop',
            style: TextStyle(
                fontSize: 30,
                fontWeight: FontWeight.bold,
            ),
            textAlign: TextAlign.center, // Pusatkan teks
            ),
        ),
        body: SingleChildScrollView(
            child: Padding(
            padding: const EdgeInsets.all(10.0),
            child: Column(
                children: <Widget>[
                Padding(
                    padding: EdgeInsets.only(top: 10.0, bottom: 10.0),
                    child: Text(
                    'Welcome!',
                    textAlign: TextAlign.center, // Pusatkan teks
                    style: TextStyle(
                        fontSize: 20, // Ukuran font yang diperkecil
                    ),
                    ),
                ),
                GridView.count(
                    primary: true,
                    padding: const EdgeInsets.all(20),
                    crossAxisSpacing: 10,
                    mainAxisSpacing: 10,
                    crossAxisCount: 3,
                    shrinkWrap: true,
                    children: items.map((ShopItem item) {
                    return ShopCard(item);
                    }).toList(),
                ),
                ],
            ),
            ),
        ),
        );
    }
    }

    class ShopItem {
    final String name;
    final IconData icon;

    ShopItem(this.name, this.icon);
    }

    class ShopCard extends StatelessWidget {
    final ShopItem item;

    const ShopCard(this.item, {Key? key}) : super(key: key);

    @override
    Widget build(BuildContext context) {
        Color backgroundColor;

        if (item.name == "Lihat Item") {
        backgroundColor = Color.fromARGB(255, 74, 124, 119);
        } else if (item.name == "Tambah Item") {
        backgroundColor = const Color.fromARGB(255, 44, 108, 161);
        } else if (item.name == "Logout") {
        backgroundColor = const Color.fromARGB(255, 112, 112, 112);
        } else {
        backgroundColor = Colors.white; // Warna latar belakang default
        }

        return Material(
        color: backgroundColor,
        child: InkWell(
            onTap: () {
            ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("Kamu telah menekan tombol ${item.name}!")));
            },
            child: Container(
            padding: const EdgeInsets.all(8),
            child: Center(
                child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                    Icon(
                    item.icon,
                    color: Colors.white,
                    size: 30.0,
                    ),
                    const Padding(padding: EdgeInsets.all(3)),
                    Text(
                    item.name,
                    textAlign: TextAlign.center,
                    style: const TextStyle(color: Colors.white),
                    ),
                ],
                ),
            ),
            ),
        ),
        );
    }
    }
    ```


4. selanjutnya saya import dari mumu_shop
``` dart
import 'package:mumu_shop/menu.dart';
```

5.  Untuk pengerjaan bonus saya menambahkan warna yang berbeda button dengan menambahkan kode berikut
```dart
 Widget build(BuildContext context) {
        Color backgroundColor;

        if (item.name == "Lihat Item") {
        backgroundColor = Color.fromARGB(255, 74, 124, 119);
        } else if (item.name == "Tambah Item") {
        backgroundColor = const Color.fromARGB(255, 44, 108, 161);
        } else if (item.name == "Logout") {
        backgroundColor = const Color.fromARGB(255, 112, 112, 112);
        } else {
        backgroundColor = Colors.white; // Warna latar belakang default
        }
```
