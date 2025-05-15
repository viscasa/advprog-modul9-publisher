<div align="center">
    <h1>MODULE 9</h1>
</div>

<div align="center">
    <img src="assets/images/burhan_pixel.png" alt="burhan" width="200"/>
</div>

<div align="center">
    <h2>Alwie Attar Elfandra</h2>
    <h2>2306241726</h2>
</div>

# 1. How much data your publisher program will send to the message broker in one run?

Dalam satu kali eksekusi, program publisher akan mengirim **5 buah pesan** ke message broker (dalam hal ini, RabbitMQ). Setiap pesan merupakan instance dari `UserCreatedEventMessage` yang berisi dua informasi: `user_id` dan `user_name`. Karena program memanggil `publish_event` sebanyak lima kali, maka total pesan yang dikirim adalah lima.

Walaupun ukuran tiap pesan akan tergantung pada hasil serialisasi dari struct tersebut (menggunakan Borsh), secara logis kita bisa menyimpulkan bahwa **lima data pengguna** (dengan `user_id` dari "1" hingga "5") akan dikirim ke antrean bernama `"user_created"`.

# 2. The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

Penggunaan URL yang sama, yaitu `"amqp://guest:guest@localhost:5672"`, baik di program **publisher** maupun **subscriber**, menunjukkan bahwa keduanya:

* Terhubung ke **broker pesan yang sama**, yaitu RabbitMQ.
* Menggunakan **komputer lokal** (`localhost`) sebagai host.
* Mengakses broker melalui **port default AMQP**, yaitu 5672.
* Melakukan autentikasi dengan **username dan password default** yaitu `"guest"` untuk keduanya.

Dengan pengaturan ini, publisher dan subscriber beroperasi dalam satu sistem komunikasi yang terhubung—publisher mengirimkan pesan ke antrean, dan subscriber mendengarkan serta memproses pesan dari antrean yang sama. Ini memungkinkan pertukaran data yang real-time dan sinkron antar komponen dalam sistem.

# Running RabbitMQ as message broker.

<div align="center">
    <img src="assets/images/running_rabbitmq.jpg" alt="rabbitmq"/>
</div>

# Sending and processing event.

<div align="center">
    <img src="assets/images/rabbitmq2.jpg" alt="rabbitmq"/>
</div>
<div align="center">
    <img src="assets/images/publisher.jpg" alt="rabbitmq"/>
</div>
<div align="center">
    <img src="assets/images/subscriber.jpg" alt="rabbitmq"/>
</div>
Pada saat message broker atau RabbitMQ berjalan, ketika program Subscriber dan Publisher kita jalankan (cargo run), maka Publisher akan mengirimkan data ke message broker dan Subscriber akan menerima data tersebut. Pada gambar di atas, kita dapat melihat bahwa Publisher mengirimkan data sekali ke message broker dan Subscriber menerimanya.

# Monitoring chart based on publisher.

<div align="center">
    <img src="assets/images/rabbitmq3.jpg" alt="rabbitmq"/>
</div>

Dari gambar, terlihat bahwa message rates akan meningkat ketika Publisher mengirimkan data ke message broker. Jika message rates tinggi, maka message broker akan menerima banyak data dari Publisher.