a. What is AMQP?

AMQP (Advanced Message Queuing Protocol) adalah protokol standar terbuka untuk pengiriman pesan antar aplikasi atau middleware. Bayangkan AMQP sebagai bahasa universal yang digunakan oleh pengirim (publisher) dan penerima (subscriber) untuk berkomunikasi melalui broker (seperti RabbitMQ).

Berbeda dengan HTTP yang bersifat request-response langsung, AMQP memungkinkan pesan dikirim ke dalam antrean (queue) sehingga sistem tetap bisa berjalan meskipun pengirim dan penerima tidak aktif di waktu yang bersamaan.

b. Understanding the Connection String

Koneksi string amqp://guest:guest@localhost:5672 terdiri dari beberapa bagian penting:

amqp://: Menandakan skema protokol yang digunakan.

guest (pertama): Adalah Username untuk autentikasi ke broker RabbitMQ. Secara default, RabbitMQ menyediakan akun "guest".

guest (kedua): Adalah Password untuk akun tersebut. Secara default, password-nya juga "guest".

localhost: Menunjukkan alamat server tempat RabbitMQ berjalan. localhost berarti broker berada di mesin yang sama dengan aplikasi yang sedang dijalankan.

:5672: Adalah Port standar yang digunakan oleh RabbitMQ untuk komunikasi pesan melalui protokol AMQP.

RabbitMQ running image: ![RabbitMQ image](image/rabbitmq.png)

Queue Message image: ![Queue Message image](image/queue_message.png)

Pada percobaan ini, jumlah pesan yang mengantre di queue (di mesin saya berjumlah 15) terjadi karena adanya ketidakseimbangan antara kecepatan publikasi dan kecepatan pemrosesan pesan:

Delay pada Subscriber: Dengan mengaktifkan thread::sleep(ten_millis), setiap pesan membutuhkan waktu minimal 1 detik untuk diproses.

Rapid Publishing: Saat publisher dijalankan berkali-kali secara cepat dalam waktu singkat, ia mengirimkan banyak pesan (misal 4 kali jalan = 20 pesan) hampir secara instan ke broker.

Queueing Mechanism: Karena subscriber hanya bisa memproses 1 pesan per detik, pesan-pesan selebihnya disimpan sementara oleh RabbitMQ di dalam memori/disk. Angka yang muncul di dashboard adalah representasi dari jumlah pesan yang sudah diterima oleh broker tetapi belum sempat diambil atau diselesaikan oleh subscriber.

Hal ini mendemonstrasikan salah satu keuntungan utama menggunakan message broker: sistem tidak langsung crash saat terjadi lonjakan beban (seperti SIAK War), melainkan pesan-pesan tersebut "diamankan" di dalam antrean sampai subscriber mampu memprosesnya satu per satu.

