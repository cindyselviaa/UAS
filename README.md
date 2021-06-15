# UAS
Uas Mobile2

import 'package:flutter/material.dart';

void main() => runApp(App13());

class App13 extends StatelessWidget {
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Cindy Selvia 6SIA1',
      home: Cindy_6SIA1(),
    );
  }
}

class Cindy_6SIA1 extends StatefulWidget {
  MyTabsState createState() => new MyTabsState();
}

class MyTabsState extends State<Cindy_6SIA1>
    with SingleTickerProviderStateMixin {
  TabController controller;
  var _scaffoldKey = new GlobalKey<ScaffoldState>();

  void initState() {
    super.initState();
    controller = new TabController(vsync: this, length: 2);
  }

  void dispose() {
    controller.dispose();
    super.dispose();
  }

  Widget build(BuildContext context) {
    return Scaffold(
      key: _scaffoldKey,
      appBar: AppBar(
        leading: IconButton(
            icon: Icon(Icons.menu),
            onPressed: () => _scaffoldKey.currentState.openDrawer()),
        title: Text('Cindy Selvia - 6SIA1'),
        actions: <Widget>[
          IconButton(icon: Icon(Icons.search), onPressed: () {}),
          IconButton(icon: Icon(Icons.more_vert), onPressed: () {}),
        ],
        bottom: TabBar(controller: controller, tabs: <Tab>[
          Tab(text: "Mahasiswa"),
          Tab(text: "Penjualan"),
        ]),
      ),
      body: TabBarView(controller: controller, children: <Widget>[
        Mahasiswa(),
        Penjualan(),
      ]),
      drawer: Menu(),
    );
  }
}

// class Mahasiswa
class Mahasiswa extends StatefulWidget {
  _MyappState createState() => _MyappState();
}

class _MyappState extends State<Mahasiswa> {
  //deklarasi variabel
  List<Widget> data = [];

  final txtnamamhs = TextEditingController();
  final txtjurusan = TextEditingController();
  final txtjkelamin = TextEditingController();

  onTambah() {
    setState(() {
      data.add(ListTile(
        leading: Icon(Icons.people),
        title: Text(txtnamamhs.text),
        subtitle: Text(txtjkelamin.text),
        trailing: Text(txtjurusan.text),
      ));
      txtnamamhs.clear();
      txtjurusan.clear();
      txtjkelamin.clear();
    });
  }

  Widget build(BuildContext context) {
    return ListView(
      children: <Widget>[
        new Container(
          padding: EdgeInsets.all(10.0),
          child: Column(
            mainAxisAlignment: MainAxisAlignment.spaceEvenly,
            children: <Widget>[
              TextField(
                controller: txtnamamhs,
                decoration: InputDecoration(hintText: 'Nama Mahasiswa'),
              ),
              TextField(
                controller: txtjurusan,
                decoration: InputDecoration(hintText: 'Jurusan'),
              ),
              TextField(
                controller: txtjkelamin,
                decoration: InputDecoration(hintText: 'Jenis Kelamin'),
              ),
              RaisedButton(child: Text("Tambah"), onPressed: onTambah),
            ],
          ),
        ),
        new Column(
          children: data,
        )
      ],
    );
  }
}

class Transaksi {
  String pelanggan;
  String barang;
  int jumlah;
  int harga;

  Transaksi({this.pelanggan, this.barang, this.jumlah, this.harga});
}

//class penjualan
class Penjualan extends StatelessWidget {
  //variabel
  final List<Transaksi> transaksi = [
    Transaksi(
        pelanggan: "Cindy Selvia", barang: "Baju", jumlah: 3, harga: 200000),
    Transaksi(pelanggan: "Cecep Hidayat", barang: "Sepatu", jumlah: 1, harga: 60000),
    Transaksi(pelanggan: "Filia Hamdani", barang: "Dompet", jumlah: 2, harga: 50000),
  ];
  Widget build(BuildContext context) {
    return ListView.builder(
      itemCount: transaksi.length,
      itemBuilder: (context, index) {
        final tr = transaksi[index];
        return ListTile(
          title: Text(tr.pelanggan),
          subtitle: Text("${tr.barang} (${tr.jumlah} pcs)"),
          onTap: () {
            Navigator.push(
                context,
                MaterialPageRoute(
                    builder: (context) =>
                        DetailTransaksi(trans: transaksi[index])));
          },
        );
      },
    );
  }
}

//class Detail Transaksi
class DetailTransaksi extends StatelessWidget {
  final Transaksi trans;

  DetailTransaksi({this.trans});

  Widget build(BuildContext context) {
    var total = trans.jumlah * trans.harga;
    return Scaffold(
      appBar: AppBar(
        title: Text("Detail Transaksi"),
      ),
      body: ListView(
        padding: EdgeInsets.all(20.0),
        children: ListTile.divideTiles(
          context: context,
          tiles: [
            ListTile(
              leading: Icon(Icons.check),
              title: Text("Nama Pelanggan"),
              trailing: Text(trans.pelanggan),
            ),
            ListTile(
              leading: Icon(Icons.check),
              title: Text("Nama Barang"),
              trailing: Text(trans.barang),
            ),
            ListTile(
              leading: Icon(Icons.check),
              title: Text("Jumlah Barang"),
              trailing: Text(trans.jumlah.toString()),
            ),
            ListTile(
              leading: Icon(Icons.check),
              title: Text("Harga"),
              trailing: Text("Rp. ${trans.harga}"),
            ),
            ListTile(
              leading: Icon(Icons.check),
              title: Text("Total"),
              trailing: Text("Rp. $total"),
            ),
          ],
        ).toList(),
      ),
    );
  }
}

// class Menu
class Menu extends StatelessWidget {
  Widget build(BuildContext context) {
    return Drawer(
        elevation: 50.0,
        child: ListView(
          padding: EdgeInsets.zero,
          children: <Widget>[
            UserAccountsDrawerHeader(
              accountName: Text('Cindy Selvia'),
              accountEmail: Text('cindyselviajb@gmail.com'),
              currentAccountPicture: Image.network(
                  'https://lh3.googleusercontent.com/ogw/ADea4I4IjzniYlEwESGl19BX-3G8E5zQaV9Tiu16X28T3Q=s32-c-mo'),
              decoration: BoxDecoration(color: Colors.blueAccent),
            ),
            ListTile(
              leading: Icon(Icons.account_circle),
              title: Text('Pemrograman Mobile-2'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.accessibility),
              title: Text('Sistem Informasi'),
              onTap: () {},
            ),
            Divider(height: 2.0),
            ListTile(
              leading: Icon(Icons.exit_to_app),
              title: Text('Sign Out'),
              onTap: () {
                Navigator.pop(context);
              },
            )
          ],
        ));
  }
}
