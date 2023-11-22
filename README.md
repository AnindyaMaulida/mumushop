<details>

<summary>Tugas 7</summary>
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
</details>

<details>

<summary>Tugas 8</summary>
 1. Jelaskan perbedaan antara Navigator.push() dan Navigator.pushReplacement(), disertai dengan contoh mengenai penggunaan kedua metode tersebut yang tepat!

Dalam pengembangan aplikasi Flutter, `Navigator.push()` dan `Navigator.pushReplacement()` adalah dua metode yang digunakan untuk mengelola navigasi antar halaman (route) dengan perbedaan utama dalam pengelolaan stack route. Ketika menggunakan `Navigator.push()`, suatu route baru ditambahkan ke dalam stack, sehingga route tersebut muncul di atas route yang sudah ada. Ini memungkinkan pengguna untuk kembali ke halaman sebelumnya dengan menekan tombol "Back" pada perangkat mereka. Sebaliknya, `Navigator.pushReplacement()` menggantikan route yang sedang ditampilkan dengan suatu route baru, tanpa memengaruhi kondisi elemen stack di bawahnya. Dengan kata lain, route yang digantikan dihapus dari stack. Metode ini berguna ketika Anda ingin mengganti halaman tanpa meninggalkan jejak halaman sebelumnya, dan jika pengguna menekan tombol "Back", mereka tidak akan kembali ke halaman yang digantikan. Pemahaman tentang perbedaan ini membantu pengembang mengontrol perilaku navigasi dan menyusun pengalaman pengguna yang lebih baik dalam aplikasi Flutter.
contoh penggunaan Navigator.push():
```dart
    if (item.name == "Tambah Produk") {
        Navigator.push(context,
            MaterialPageRoute(builder: (context) => const ShopFormPage()));
    }
```

contoh penggunan `Navigator.pushReplacement()`:
```dart
onTap: () {
        Navigator.pushReplacement(
        context,
        MaterialPageRoute(
            builder: (context) => MyHomePage(),
        ));
    },
```

 2. Jelaskan masing-masing layout widget pada Flutter dan konteks penggunaannya masing-masing!
 - AppBar: AppBar adalah layout widget yang menyediakan bilah atas (bar) untuk menampilkan judul atau elemen-elemen lainnya dalam menampilkan judul "Form Tambah Produk" di tengah bilah atas aplikasi.
 - Drawer: Drawer adalah layout widget yang menyediakan navigasi sisi yang dapat digeser (drawer) yang diintegrasikan ke dalam aplikasi sebagai navigasi sisi.
 - Form: Form adalah layout widget yang digunakan untuk membuat formulir dengan validasi untuk membungkus seluruh bagian formulir, memanfaatkan formKey untuk validasi.
 - SingleChildScrollView: SingleChildScrollView adalah layout widget yang memungkinkan kontennya dapat digulir (scrollable) untuk memastikan tata letak halaman tetap dapat digulir jika kontennya melebihi ruang yang tersedia.
 - Column: Column adalah layout widget yang menyusun anak-anaknya dalam satu kolom untuk menyusun elemen-elemen formulir secara vertikal.
 - Padding: Padding adalah layout widget yang menambahkan ruang putih di sekeliling widget anaknya untuk memberikan ruang putih di sekitar TextFormField.
 - TextFormField: TextFormField adalah widget formulir yang mengumpulkan input teks dari pengguna untuk mengumpulkan nama produk, harga, dan deskripsi dari pengguna dengan memberikan validasi.
 - Align: Align adalah layout widget yang mengatur posisi anaknya sesuai dengan parameter alignment yang diberikan untuk menempatkan tombol "Save" di bagian bawah tengah halaman.
 - ElevatedButton: ElevatedButton adalah layout widget yang menampilkan tombol yang diangkat untuk digunakan sebagai tombol "Save" dengan warna latar belakang tertentu ketika ditekan.
 - AlertDialog: AlertDialog adalah layout widget yang menampilkan dialog dengan judul dan konten tertentu untuk menampilkan informasi produk yang berhasil tersimpan setelah pengguna menekan tombol "Save".

 3. Sebutkan apa saja elemen input pada form yang kamu pakai pada tugas kali ini dan jelaskan mengapa kamu menggunakan elemen input tersebut!
 - ```TextFormField ```
 Dalam tugas ini penggunaan TextFormField digunakan untuk input pada form untuk mengisi nama produk, harga, dan deskripsi. Dengan validator agar field tersebut tidak boleh kosong dan sesuai dengan model nya seperti harga harus berupa angka.
 - ```ElevatedButton ```
 Dalam tugas ini penggunaan berfungsi sebagai tombol "Simpan." Saat tombol diklik, aplikasi akan melakukan pemeriksaan terhadap kelengkapan dan validitas semua kolom input menggunakan _formKey.currentState!.validate(). Jika berhasil maka akan memberikan informasi bahwa data produk telah berhasil disimpan.

 4. Bagaimana penerapan clean architecture pada aplikasi Flutter?
 Clean Architecture adalah pendekatan pengembangan perangkat lunak untuk menciptakan aplikasi bersih, modular, dan mudah diuji. Keuntungan penggunaan Clean Architecture melibatkan pemisahan tanggung jawab, meningkatkan keterbacaan, memudahkan pemeliharaan kode, dan kemampuan untuk mengelola kompleksitas aplikasi dengan efisien. Struktur yang terorganisir dengan baik memfasilitasi pengembangan dan pemeliharaan kode.

 **Pembagian Lapisan Utama:**
 - Lapisan Presentasi (UI): berfungsi menangani interaksi pengguna dan menampilkan antarmuka pengguna, berisi komponen seperti widget, layar, dan tampilan, serta menggunakan pola manajemen state seperti BLoC, Provider, atau Redux.
 - Lapisan Domain (Bisnis): Lapisan ini berfungsi untuk menyimpan aturan bisnis inti aplikasi yang berisi entitas sebagai model data bisnis serta kasus Penggunaan (Use Case) menggambarkan aksi pengguna.
 - Lapisan Data: Lapisan ini berfungsi untuk mengimplementasi repositori sesuai kontrak dari lapisan domain, sumber data berkomunikasi dengan sumber data eksternal seperti API atau database. Model data merepresentasikan struktur data yang digunakan oleh sumber data.

 5. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial)
    1. **Drawer Menu**
    pertama saya membuat folder bernama `widgets` dan membuat file bernama `left_drawer.dart` yang berisi navigasi ke halaman-halaman lain pada aplikasi. Dengan menambahkan kode berikut pada file ` `:
    ```dart
    import 'package:flutter/material.dart';
    import 'package:mumu_shop/screens/menu.dart';
    import 'package:mumu_shop/screens/shoplist_form.dart';

    class LeftDrawer extends StatelessWidget {
    const LeftDrawer({super.key});

    @override
    Widget build(BuildContext context) {
        return Drawer(
        child: ListView(
            children: [
            const DrawerHeader(
                // TODO: Bagian drawer header
                decoration: BoxDecoration(
                color: Color.fromARGB(255, 88, 116, 123),
                ),
                child: Column(
                children: [
                    Text(
                    'mumu_shop',
                    textAlign: TextAlign.center,
                    style: TextStyle(
                        fontSize: 30, //
                        fontWeight: FontWeight.bold,
                        color: Colors.white,
                    ),
                    ),
                    Padding(padding: EdgeInsets.all(10)),
                    Text("Catat seluruh keperluan belanjamu di sini!",
                        // TODO: Tambahkan gaya teks dengan center alignment, font ukuran 15, warna putih, dan weight biasa
                        textAlign: TextAlign.center,
                        style: TextStyle(
                        fontSize: 15,
                        color: Colors.white,
                        fontWeight: FontWeight.normal,
                        ),
                        ),
                ],
                ),
            ),
            
            // TODO: Bagian routing
            ListTile(
                leading: const Icon(Icons.home_outlined),
                title: const Text('Halaman Utama'),
                // Bagian redirection ke MyHomePage
                onTap: () {
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(
                        builder: (context) => MyHomePage(),
                    ));
                },
            ),
            ListTile(
                leading: const Icon(Icons.add_shopping_cart),
                title: const Text('Tambah Produk'),
                // Bagian redirection ke ShopFormPage
                onTap: () {
                /*
                TODO: Buatlah routing ke ShopFormPage di sini,
                setelah halaman ShopFormPage sudah dibuat.
                */
                Navigator.pushReplacement(
                    context,
                    MaterialPageRoute(
                        builder: (context) => ShopFormPage(),
                    ));
                },
            ),
            
            ],
        ),
        );
    }
    }
    ```
    2. **Elemen Input dan Form**
    menambahkan input field yang ada pada flutter dengan kode `flutter create --sample=widgets.Form.1 form_sample`

    3. **Pembuatan Form dan Data**
    dan dalam pembuatan form dan data saya membuat file bernama `shoplist_form.dart.`di dalam folder baru bernama `screens` dengan menambahkan kode berikut:
    ```dart
    import 'package:flutter/material.dart';
    import 'package:mumu_shop/widgets/left_drawer.dart';

    class ShopFormPage extends StatefulWidget {
    const ShopFormPage({super.key});

    @override
    State<ShopFormPage> createState() => _ShopFormPageState();
    }

    class _ShopFormPageState extends State<ShopFormPage> {
    final _formKey = GlobalKey<FormState>();
    String _name = "";
    int _price = 0;
    String _description = "";

    @override
    Widget build(BuildContext context) {
        return Scaffold(
        appBar: AppBar(
            title: const Center(
            child: Text(
                'Form Tambah Produk',
            ),
            ),
            backgroundColor: Color.fromARGB(255, 88, 116, 123),
            foregroundColor: Colors.white,
        ),
        // OK TODO: Tambahkan drawer yang sudah dibuat di sini
        drawer: const LeftDrawer(),
        body: Form(
            key: _formKey,
            child: SingleChildScrollView(
            child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                    decoration: InputDecoration(
                        hintText: "Nama Produk",
                        labelText: "Nama Produk",
                        border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(5.0),
                        ),
                    ),
                    onChanged: (String? value) {
                        setState(() {
                        _name = value!;
                        });
                    },
                    validator: (String? value) {
                        if (value == null || value.isEmpty) {
                        return "Nama tidak boleh kosong!";
                        }
                        return null;
                    },
                    ),
                ),
                Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                    decoration: InputDecoration(
                        hintText: "Harga",
                        labelText: "Harga",
                        border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(5.0),
                        ),
                    ),
                    // OK TODO: Tambahkan variabel yang sesuai
                    onChanged: (String? value) {
                        setState(() {
                        _price = int.parse(value!);
                        });
                    },
                    validator: (String? value) {
                        if (value == null || value.isEmpty) {
                        return "Harga tidak boleh kosong!";
                        }
                        if (int.tryParse(value) == null) {
                        return "Harga harus berupa angka!";
                        }
                        return null;
                    },
                    ),
                ),
                Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: TextFormField(
                    decoration: InputDecoration(
                        hintText: "Deskripsi",
                        labelText: "Deskripsi",
                        border: OutlineInputBorder(
                        borderRadius: BorderRadius.circular(5.0),
                        ),
                    ),
                    onChanged: (String? value) {
                        setState(() {
                        // OK TODO: Tambahkan variabel yang sesuai
                        _description = value!;
                        });
                    },
                    validator: (String? value) {
                        if (value == null || value.isEmpty) {
                        return "Deskripsi tidak boleh kosong!";
                        }
                        return null;
                    },
                    ),
                ),
                Align(
                    alignment: Alignment.bottomCenter,
                    child: Padding(
                    padding: const EdgeInsets.all(8.0),
                    child: ElevatedButton(
                        style: ButtonStyle(
                        backgroundColor:
                            MaterialStateProperty.all(Color.fromARGB(255, 88, 116, 123)),
                        ),
                        onPressed: () {
                        if (_formKey.currentState!.validate()) {
                            showDialog(
                            context: context,
                            builder: (context) {
                                return AlertDialog(
                                title: const Text('Produk berhasil tersimpan'),
                                content: SingleChildScrollView(
                                    child: Column(
                                    crossAxisAlignment:
                                        CrossAxisAlignment.start,
                                    children: [
                                        Text('Nama: $_name'),
                                        // OK TODO: Munculkan value-value lainnya
                                        Text('Harga: $_price'),
                                        Text('Deskripsi: $_description'),
                                    ],
                                    ),
                                ),
                                actions: [
                                    TextButton(
                                    child: const Text('OK'),
                                    onPressed: () {
                                        Navigator.pop(context);
                                    },
                                    ),
                                ],
                                );
                            },
                            );
                            _formKey.currentState!.reset();
                        }

                        },
                        child: const Text(
                        "Save",
                        style: TextStyle(color: Colors.white),
                        ),
                    ),
                    ),
                ),
                ]
            ),  
            ),
        ),
        );
    }
    }
    ```
    4. **Memunculkan data**
    menambahkan kode berikut kedalam file `shoplist_form.dart`:
    ```dart
     child: ElevatedButton(
        style: ButtonStyle(
            backgroundColor:
                MaterialStateProperty.all(Color.fromARGB(255, 88, 116, 123)),
        ),
        onPressed: () {
            if (_formKey.currentState!.validate()) {
            showDialog(
                context: context,
                builder: (context) {
                return AlertDialog(
                    title: const Text('Produk berhasil tersimpan'),
                    content: SingleChildScrollView(
                    child: Column(
                        crossAxisAlignment:
                            CrossAxisAlignment.start,
                        children: [
                        Text('Nama: $_name'),
                        // OK TODO: Munculkan value-value lainnya
                        Text('Harga: $_price'),
                        Text('Deskripsi: $_description'),
                        ],
                    ),
                    ),
                    actions: [
                    TextButton(
                        child: const Text('OK'),
                        onPressed: () {
                        Navigator.pop(context);
                        },
                    ),
                    ],
                );
                },
            );
            _formKey.currentState!.reset();
            }

        },
        child: const Text(
            "Save",
            style: TextStyle(color: Colors.white),
        ),
        ),
    ),
    ```
    4. **Navigasi Pada Tombol**
    untuk melakukan navigasi ke route lain saya menmbahkan kode berikut pada file `shop_card.dart`:
    ```dart
    import 'package:flutter/material.dart';
    import 'package:mumu_shop/screens/shoplist_form.dart';

    class ShopItem {
    final String name;
    final IconData icon;
    final Color color;

    ShopItem(this.name, this.icon, this.color);
    }

    class ShopCard extends StatelessWidget {
    final ShopItem item;

    const ShopCard(this.item, {super.key}); // Constructor

    @override
    Widget build(BuildContext context) {
        return Material(
        color: item.color,
        child: InkWell(
            // Area responsive terhadap sentuhan
            onTap: () {
            // Memunculkan SnackBar ketika diklik
            ScaffoldMessenger.of(context)
                ..hideCurrentSnackBar()
                ..showSnackBar(SnackBar(
                    content: Text("Kamu telah menekan tombol ${item.name}!")));

            // Navigate ke route yang sesuai (tergantung jenis tombol)
            if (item.name == "Tambah Produk") {
                // TODO: Gunakan Navigator.push untuk melakukan navigasi ke MaterialPageRoute yang mencakup ShopFormPage.
                Navigator.push(
                context,
                MaterialPageRoute(builder: (context) => ShopFormPage()),
                );
            }
            },
            child: Container(
            // Container untuk menyimpan Icon dan Text
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
</details>


<summary>Tugas 9</summary>
1. Apakah bisa kita melakukan pengambilan data JSON tanpa membuat model terlebih dahulu? Jika iya, apakah hal tersebut lebih baik daripada membuat model sebelum melakukan pengambilan data JSON?

2. Jelaskan fungsi dari CookieRequest dan jelaskan mengapa instance CookieRequest perlu untuk dibagikan ke semua komponen di aplikasi Flutter.
CookieRequest dalam flutter biasanya digunakan untuk mengelola state otentikasi atau informasi lainnya yang diperlukan untuk berinteraksi dengan backend. 

CookieRequest digunakan untuk melakukan permintaan HTTP pada aplikasi Flutter yang dapat mengatur dan menyimpan informasi otentikasi atau data lain yang diperlukan untuk permintaan HTTP. Membagikan instance CookieRequest ke seluruh komponen menggunakan Provider sehingga mudah untuk diakses dan dikelola di seluruh aplikasi dan penggantian implementasi CookieRequest atau pembaruan konfigurasi dengan mudah tanpa perlu memodifikasi banyak bagian dari kode.

contoh penggunaan cookieRequest pada `main.dart`:
```dart
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return Provider(
      create: (_) {
          CookieRequest request = CookieRequest();
          return request;
      },
```

3. Jelaskan mekanisme pengambilan data dari JSON hingga dapat ditampilkan pada Flutter.
pertama kita harus memastikan sudah ada data JSON dengan menambahkan produk, kemudian jika sudah ada untuk mengambil data JSON tersebut dari WEB API biasanya menggunakan HTTP GET atau POST. Setelah mengambil data JSON dan data tersebut diterima oleh flutter, kita menambahkan fungsi jsonDecode() dari paket dart:convert dan membuat fungsi widget pada flutter seperti LisView agar data JSON tersebut dapat ditampilan untuk user pada flutter. 

pada tahap ini saya membuka website `Quicktype` 
4. Jelaskan mekanisme autentikasi dari input data akun pada Flutter ke Django hingga selesainya proses autentikasi oleh Django dan tampilnya menu pada Flutter.
Mekanisme autentikasi dari input data akun pada Flutter ke Django yaitu dengan melibatkan permintaan HTTP dari Flutter ke otentikasi Django, seperti /api/token/. Setelah pengguna memasukkan data akun kemudian Django berhasil memverifikasi kredensial, Django mengirimkan token akses ke Flutter. Token ini disimpan di Flutter dan digunakan untuk otentikasi setiap permintaan HTTP selanjutnya. Dengan menggunakan token akses, Flutter dapat mengidentifikasi pengguna yang terotentikasi dan menavigasinya ke halaman atau menu yang sesuai dengan status otentikasinya, seperti menampilkan menu terotentikasi atau memberikan akses ke fitur-fitur khusus.

5. Sebutkan seluruh widget yang kamu pakai pada tugas ini dan jelaskan fungsinya masing-masing.
Widget

- Scaffold: Ini adalah widget utama yang biasanya digunakan sebagai kerangka dasar tata letak material design.
- AppBar: Sebuah widget yang biasanya digunakan sebagai bagian atas Scaffold yang berisi judul dan beberapa tindakan.
- Padding: Widget ini digunakan untuk memberikan padding ke widget anaknya.
- Column: Widget ini digunakan untuk menampilkan anak-anaknya dalam tata letak vertikal.
- Text: Widget yang digunakan untuk menampilkan teks.
- Icon: Widget yang digunakan untuk menampilkan ikon.
- LeftDrawer: Widget yang digunakan untuk menampilkan drawer pada sebelah kiri bagian.
- FutureBuilder: Widget ini digunakan untuk membuat widget berdasarkan hasil Future.
- Center: Widget ini digunakan untuk meletakkan ke tengah-tengah.
- CircularProgressIndicator: Widget ini digunakan untuk menampilkan indikator progres yang berputar.
- ListView.builder: Widget yang digunakan untuk membuat daftar yang dapat digulir.
- MaterialApp: Widget yang menyediakan fitur-fitur dasar dari Material Design, seperti tema, navigasi, dan gesture.
- Container: Widget yang menyediakan kotak untuk menampung widget lainnya dengan berbagai atribut, seperti padding, margin, alignment, dan decoration.
- MaterialPageRoute: Widget yang menyediakan transisi material design antara halaman.
- Navigator: Widget yang menyediakan mekanisme untuk mengelola tumpukan widget yang dapat dinavigasi, seperti halaman atau layar.
- ListTile: Widget yang menyediakan sebuah item yang dapat diklik pada daftar, biasanya digunakan untuk menampilkan ikon, teks, dan tindakan.
- MyApp: Widget yang merupakan subclass dari StatelessWidget. Widget ini merupakan widget utama yang digunakan untuk menjalankan aplikasi Flutter.
- StatelessWidget: Widget yang merupakan superclass dari MyApp. Widget ini merupakan widget yang tidak memiliki state atau kondisi yang berubah-ubah.
- Provider: Widget yang digunakan untuk menyediakan sebuah objek yang dapat diakses oleh widget-widget lainnya melalui context. Widget ini digunakan untuk menyediakan objek CookieRequest yang digunakan untuk melakukan request ke server menggunakan cookie.
- MaterialApp: Widget yang menyediakan fitur-fitur dasar dari Material Design, seperti tema, navigasi, dan gesture. Widget ini digunakan untuk menentukan judul, tema, dan halaman utama aplikasi.
- LoginPage: Widget yang digunakan untuk menampilkan halaman login aplikasi. Widget ini merupakan subclass dari StatefulWidget yang memiliki state atau kondisi yang berubah-ubah.

6. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step! (bukan hanya sekadar mengikuti tutorial).
pada step ini saya membuat django app dengan menjalankan perintah berikut: 
`python3 manage.py startapp authentication`

serta menambahkan beberapa hal yang diperlukan seperti `authentication`, `corsheaders`, dan `corsheaders.middleware.CorsMiddleware` pada settings.py

selanjutnya mengisi views.py pada folder authentication pada django dengan kode berikut:
```python
from django.shortcuts import render

# Create your views here.
from django.shortcuts import render
from django.contrib.auth import authenticate, login as auth_login
from django.http import JsonResponse
from django.views.decorators.csrf import csrf_exempt
from django.contrib.auth import logout as auth_logout

@csrf_exempt
def login(request):
    username = request.POST['username']
    password = request.POST['password']
    user = authenticate(username=username, password=password)
    if user is not None:
        if user.is_active:
            auth_login(request, user)
            # Status login sukses.
            return JsonResponse({
                "username": user.username,
                "status": True,
                "message": "Login sukses!"
                # Tambahkan data lainnya jika ingin mengirim data ke Flutter.
            }, status=200)
        else:
            return JsonResponse({
                "status": False,
                "message": "Login gagal, akun dinonaktifkan."
            }, status=401)

    else:
        return JsonResponse({
            "status": False,
            "message": "Login gagal, periksa kembali email atau kata sandi."
        }, status=401)
    

@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logout berhasil!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout gagal."
        }, status=401)
```

dan mengisi file login.dart pada folder screens:
```dart
import 'package:mumu_shop/screens/menu.dart';
import 'package:flutter/material.dart';
import 'package:pbp_django_auth/pbp_django_auth.dart';
import 'package:provider/provider.dart';

void main() {
    runApp(const LoginApp());
}

class LoginApp extends StatelessWidget {
const LoginApp({super.key});

@override
Widget build(BuildContext context) {
    return MaterialApp(
        title: 'Login',
        theme: ThemeData(
            primarySwatch: Colors.blue,
    ),
    home: const LoginPage(),
    );
    }
}

class LoginPage extends StatefulWidget {
    const LoginPage({super.key});

    @override
    _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
    final TextEditingController _usernameController = TextEditingController();
    final TextEditingController _passwordController = TextEditingController();

    @override
    Widget build(BuildContext context) {
        final request = context.watch<CookieRequest>();
        return Scaffold(
            appBar: AppBar(
                title: const Text('Login'),
            ),
            body: Container(
                padding: const EdgeInsets.all(16.0),
                child: Column(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                        TextField(
                            controller: _usernameController,
                            decoration: const InputDecoration(
                                labelText: 'Username',
                            ),
                        ),
                        const SizedBox(height: 12.0),
                        TextField(
                            controller: _passwordController,
                            decoration: const InputDecoration(
                                labelText: 'Password',
                            ),
                            obscureText: true,
                        ),
                        const SizedBox(height: 24.0),
                        ElevatedButton(
                            onPressed: () async {
                                String username = _usernameController.text;
                                String password = _passwordController.text;

                                // Cek kredensial
                                // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
                                // Untuk menyambungkan Android emulator dengan Django pada localhost,
                                // gunakan URL http://10.0.2.2/
                                final response = await request.login("http://127.0.0.1:8000/auth/login/", {
                                'username': username,
                                'password': password,
                                });
                    
                                if (request.loggedIn) {
                                    String message = response['message'];
                                    String uname = response['username'];
                                    Navigator.pushReplacement(
                                        context,
                                        MaterialPageRoute(builder: (context) => MyHomePage()),
                                    );
                                    ScaffoldMessenger.of(context)
                                        ..hideCurrentSnackBar()
                                        ..showSnackBar(
                                            SnackBar(content: Text("$message Selamat datang, $uname.")));
                                    } else {
                                    showDialog(
                                        context: context,
                                        builder: (context) => AlertDialog(
                                            title: const Text('Login Gagal'),
                                            content:
                                                Text(response['message']),
                                            actions: [
                                                TextButton(
                                                    child: const Text('OK'),
                                                    onPressed: () {
                                                        Navigator.pop(context);
                                                    },
                                                ),
                                            ],
                                        ),
                                    );
                                }
                            },
                            child: const Text('Login'),
                        ),
                    ],
                ),
            ),
        );
    }
}
```

dan menambahkan kode berikut dengan cara membuka website `Quicktype`
dengan mengganti bahasanya menjadi dart dan sesuaikan nama nya disini saya menggunakan product. 
```dart
import 'dart:convert';

List<Product> productFromJson(String str) => List<Product>.from(json.decode(str).map((x) => Product.fromJson(x)));

String productToJson(List<Product> data) => json.encode(List<dynamic>.from(data.map((x) => x.toJson())));

class Product {
    Model model;
    int pk;
    Fields fields;

    Product({
        required this.model,
        required this.pk,
        required this.fields,
    });

    factory Product.fromJson(Map<String, dynamic> json) => Product(
        model: modelValues.map[json["model"]]!,
        pk: json["pk"],
        fields: Fields.fromJson(json["fields"]),
    );

    Map<String, dynamic> toJson() => {
        "model": modelValues.reverse[model],
        "pk": pk,
        "fields": fields.toJson(),
    };
}

class Fields {
    String name;
    DateTime dateAdded;
    int price;
    String description;
    int user;

    Fields({
        required this.name,
        required this.dateAdded,
        required this.price,
        required this.description,
        required this.user,
    });

    factory Fields.fromJson(Map<String, dynamic> json) => Fields(
        name: json["name"],
        dateAdded: DateTime.parse(json["date_added"]),
        price: json["price"],
        description: json["description"],
        user: json["user"],
    );

    Map<String, dynamic> toJson() => {
        "name": name,
        "date_added": "${dateAdded.year.toString().padLeft(4, '0')}-${dateAdded.month.toString().padLeft(2, '0')}-${dateAdded.day.toString().padLeft(2, '0')}",
        "price": price,
        "description": description,
        "user": user,
    };
}

enum Model {
    MAIN_PRODUCT
}

final modelValues = EnumValues({
    "main.product": Model.MAIN_PRODUCT
});

class EnumValues<T> {
    Map<String, T> map;
    late Map<T, String> reverseMap;

    EnumValues(this.map);

    Map<T, String> get reverse {
        reverseMap = map.map((k, v) => MapEntry(v, k));
        return reverseMap;
    }
}

```
dan menambahkan kode berikut pada file list_product.dart:
```dart
import 'package:flutter/material.dart';
import 'package:http/http.dart' as http;
import 'package:mumu_shop/models/product.dart';
import 'dart:convert';
import 'package:mumu_shop/widgets/left_drawer.dart';

class ProductPage extends StatefulWidget {
    const ProductPage({Key? key}) : super(key: key);

    @override
    _ProductPageState createState() => _ProductPageState();
}

class _ProductPageState extends State<ProductPage> {
Future<List<Product>> fetchProduct() async {
    // TODO: Ganti URL dan jangan lupa tambahkan trailing slash (/) di akhir URL!
    var url = Uri.parse(
        'http://127.0.0.1:8000/json/');
    var response = await http.get(
        url,
        headers: {"Content-Type": "application/json"},
    );

    // melakukan decode response menjadi bentuk json
    var data = jsonDecode(utf8.decode(response.bodyBytes));

    // melakukan konversi data json menjadi object Product
    List<Product> list_product = [];
    for (var d in data) {
        if (d != null) {
            list_product.add(Product.fromJson(d));
        }
    }
    return list_product;
}

@override
Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
        title: const Text('Product'),
        ),
        drawer: const LeftDrawer(),
        body: FutureBuilder(
            future: fetchProduct(),
            builder: (context, AsyncSnapshot snapshot) {
                if (snapshot.data == null) {
                    return const Center(child: CircularProgressIndicator());
                } else {
                    if (!snapshot.hasData) {
                    return const Column(
                        children: [
                        Text(
                            "Tidak ada data produk.",
                            style:
                                TextStyle(color: Color(0xff59A5D8), fontSize: 20),
                        ),
                        SizedBox(height: 8),
                        ],
                    );
                } else {
                    return ListView.builder(
                        itemCount: snapshot.data!.length,
                        itemBuilder: (_, index) => Container(
                                margin: const EdgeInsets.symmetric(
                                    horizontal: 16, vertical: 12),
                                padding: const EdgeInsets.all(20.0),
                                child: Column(
                                mainAxisAlignment: MainAxisAlignment.start,
                                crossAxisAlignment: CrossAxisAlignment.start,
                                children: [
                                    Text(
                                    "${snapshot.data![index].fields.name}",
                                    style: const TextStyle(
                                        fontSize: 18.0,
                                        fontWeight: FontWeight.bold,
                                    ),
                                    ),
                                    const SizedBox(height: 10),
                                    Text("${snapshot.data![index].fields.price}"),
                                    const SizedBox(height: 10),
                                    Text(
                                        "${snapshot.data![index].fields.description}")
                                ],
                                ),
                            ));
                    }
                }
            }));
    }
}
```

setelah menambahkan kode pada flutter, selanjutnya menambahkan beberapa kode pada django
untuk menambahkan create product flutter bisa dijalankan tambahkan kode berikut pada views.py dan menambahkan path pada urls.py:
```python 
@csrf_exempt
def create_product_flutter(request):
    if request.method == 'POST':
        
        data = json.loads(request.body)

        new_product = Product.objects.create(
            user = request.user,
            name = data["name"],
            price = int(data["price"]),
            description = data["description"]
        )

        new_product.save()

        return JsonResponse({"status": "success"}, status=200)
    else:
        return JsonResponse({"status": "error"}, status=401)

```
setelah semua selesai menyelesaikan untuk logout dengan menambahkan kode berikut pada file views.py pada authentication:
```python
from django.contrib.auth import logout as auth_logout
...
@csrf_exempt
def logout(request):
    username = request.user.username

    try:
        auth_logout(request)
        return JsonResponse({
            "username": username,
            "status": True,
            "message": "Logout berhasil!"
        }, status=200)
    except:
        return JsonResponse({
        "status": False,
        "message": "Logout gagal."
        }, status=401)

```

setelah semua selesai, jalankan flutter dan django secara bersamaan agar bisa dijalankan. 