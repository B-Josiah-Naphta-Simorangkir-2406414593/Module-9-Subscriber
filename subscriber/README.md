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