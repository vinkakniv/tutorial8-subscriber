# Advanced Programming - Tutorial


------------
## Overview

This repository contains the code and reflections for Tutorial 8 in Advanced Programming course by Vinka Alrezky As (NPM: 2206820200)❄️
- [Tutorial 8 - Subscriber](https://github.com/vinkakniv/tutorial8-subscriber)
- [Tutorial 8 - Publisher](https://github.com/vinkakniv/tutorial8-publisher)
------------
# Tutorial 8 - Subscriber

### _Reflection_

> a. what is amqp?

AMQP (_Advanced Message Queuing Protocol_) adalah _open standard application layer protocol_ yang dirancang untuk _message-oriented middleware_. Protokol ini membantu dalam pemindahan pesan yang efisien dan aman antara dua atau lebih titik, mendukung fitur seperti _queuing_, _routing_, _reliability_, dan _security_. Ini sangat berguna dalam _enterprise applications_ untuk memastikan komunikasi data yang _reliable_ dan teratur antar komponen dalam _distributed system_.  Protokol ini memungkinkan berbagai sistem untuk berkomunikasi dengan efisiensi tinggi meskipun menggunakan teknologi yang berbeda.
Dengan menggunakan AMQP, perusahaan dapat lebih mudah mengelola dan memelihara arsitektur TI yang besar dan terdistribusi. Kelebihan utama dari AMQP termasuk kemampuannya untuk memastikan integritas data dan mengoptimalkan pengiriman pesan dalam skala besar.

> b. what it means? guest:guest@localhost:5672 , what is the first guest, and what is
the second guest, and what is localhost:5672 is for?

String `guest:guest@localhost:5672` adalah _connection_ string yang digunakan untuk _connect_ ke server AMQP. Formatnya adalah `username:password@hostname:port`. Dalam kasus ini, `guest` pertama adalah _username_, `guest` yang kedua adalah _password_. Bagian `localhost:5672` adalah nama host dan port di mana server AMQP berjalan. `localhost` berarti server berjalan di mesin yang sama, dan `5672` adalah port default untuk AMQP. Ini menandakan bahwa server berjalan pada mesin yang sama dengan klien, memudahkan pengembangan dan pengujian lokal tanpa perlu koneksi jaringan eksternal. Koneksi seperti ini sering digunakan dalam pengaturan pengembangan untuk mempermudah konfigurasi.

![](https://imgur.com/dpqK0co.png)

Grafik di atas menunjukkan interaksi dinamis antara aplikasi publisher dan consumer. Dari hasil pengujian ini, terlihat bahwa setelah menjalankan aplikasi subscriber dengan perintah `cargo run`, dan kemudian menjalankan aplikasi publisher beberapa kali. Setiap kali perintah cargo run pada publisher dieksekusi, event baru dihasilkan dan dikirim ke _queue_.

Grafik 'Queued messages' yang ditampilkan menggambarkan peningkatan jumlah pesan yang terantri, mencapai angka tujuh. Angka ini menunjukkan bahwa terdapat tujuh pesan yang belum diolah oleh consumer pada satu waktu. Hal ini menandakan bahwa walaupun pesan berhasil diantarkan ke _queue_, consumer mengolahnya secara bertahap, yang menghasilkan penumpukan sementara pesan dalam _queue_.

Grafik 'Message Rates' menampilkan dua aspek penting: laju pesan yang dipublikasikan (Publish rate) dan laju pesan yang diakui oleh consumer (Acknowledge rate).
Terlihat bahwa ada peningkatan tajam dalam laju pengiriman pesan setiap kali aplikasi publisher dijalankan. Hal ini menandakan bahwa publisher berhasil mengirimkan event ke queue dengan cepat. Namun, tingkat pengakuan pesan oleh consumer cenderung lebih stabil dan terjadi dengan laju yang lebih lambat, yang menunjukkan bahwa consumer sedang mengolah pesan-pesan tersebut secara bertahap.