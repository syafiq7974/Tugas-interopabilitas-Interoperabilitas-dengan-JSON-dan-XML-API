NAMA  : Syafiq Burhanuddin
KELAS  : 2A TRPL
NIM : 362358302068

Tugas
Pengembangan API :
Tambahkan endpoint baru untuk menambahkan data baru ke dalam JSON dan XML API. 
•	Buat endpoint GET di API JSON dan XML yang mengembalikan daftar item (misalnya, daftar buku atau daftar film). 
•	Buat endpoint POST di API JSON dan XML yang memungkinkan pengguna menambahkan item baru ke daftar. 

Bagian 1: API JSON Menggunakan Node.js
const express = require('express');
const app = express();
const port = 3000;

app.use(express.json());

let items = [
  { id: 1, name: "Book 1", author: "Author A" },
  { id: 2, name: "Book 2", author: "Author B" }
];

// GET endpoint untuk mengambil daftar item
app.get('/items', (req, res) => {
  res.json(items);
});

// POST endpoint untuk menambahkan item baru
app.post('/items', (req, res) => {
  const newItem = req.body;
  newItem.id = items.length + 1;
  items.push(newItem);
  res.status(201).json(newItem);
});

app.listen(port, () => {
  console.log(`Server berjalan di http://localhost:${port}`);
});

Hasilnya :
 ![image](https://github.com/user-attachments/assets/52779c40-95c6-4560-8cd2-0727510a5ebf)
 buat file baru dengan json_xml_to.php
2.	Masukkan kode berikut:
<?php
$json_data = file_get_contents('http://localhost/praktikumjson/api.php'); // Ganti dengan URL API JSON yang sesuai
$array_data = json_decode($json_data, true);

$xml = new SimpleXMLElement('<items/>');

foreach ($array_data as $item) {
    $item_xml = $xml->addChild('item');
    $item_xml->addChild('id', $item['id']);
    $item_xml->addChild('name', $item['name']);
    $item_xml->addChild('author', $item['author']);
}

header('Content-Type: application/xml');
echo $xml->asXML();
?>
hasilnya
![image](https://github.com/user-attachments/assets/e7bd0d5a-7542-4ea6-a542-499531c7d58f)


