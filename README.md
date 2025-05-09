## ✍️ Refleksi

1. **Apa perbedaan utama antara unary, server streaming, dan bi-directional streaming dalam RPC? Dan kapan masing-masing paling tepat digunakan?**
Perbedaannya terletak pada arah dan jumlah data yang dikirim. Unary hanya mengirim satu request dan menerima satu response, cocok untuk operasi sederhana seperti registrasi atau pembayaran. Server streaming memungkinkan client mengirim satu request lalu server membalas dengan stream data — contohnya saat menampilkan riwayat transaksi. Sedangkan bi-directional streaming memungkinkan client dan server saling bertukar data secara real-time, sangat sesuai untuk fitur chat atau kolaborasi langsung.

2. **Apa saja pertimbangan keamanan yang perlu diperhatikan saat membangun layanan gRPC di Rust?**
Beberapa hal penting mencakup penggunaan TLS untuk mengenkripsi data, implementasi autentikasi dan otorisasi seperti JWT untuk mengatur akses, serta validasi input agar mencegah eksploitasi. Selain itu, kita juga harus memperhatikan bagaimana menangani error dan menjaga kerahasiaan data pengguna.

3. **Apa tantangan dalam menangani streaming dua arah di Rust gRPC, khususnya untuk aplikasi seperti chat?**
Tantangan utamanya adalah sinkronisasi antara pengiriman dan penerimaan pesan. Kita harus memastikan bahwa client dan server bisa saling merespons tanpa terjadi konflik atau kehilangan data. Selain itu, menjaga koneksi tetap stabil dalam waktu lama dan mengatur banyak stream secara bersamaan juga bisa menjadi kompleks.

4. **Apa kelebihan dan kekurangan penggunaan `tokio_stream::wrappers::ReceiverStream` untuk response streaming?**
ReceiverStream memudahkan kita untuk membungkus channel menjadi stream yang bisa digunakan oleh gRPC. Kelebihannya, implementasinya cukup sederhana dan cocok untuk skenario async. Tapi kekurangannya, kita harus hati-hati dalam manajemen resource-nya, terutama jika jumlah pesan yang dikirim cukup banyak atau terus-menerus.

5. **Bagaimana struktur kode gRPC di Rust bisa dibuat agar mudah dikembangkan dan dirawat?**
Salah satu caranya adalah dengan memisahkan tiap service ke dalam modul yang berbeda, lalu menyusun logic bisnis secara terpisah dari definisi gRPC-nya. Dengan begitu, kita bisa mempermudah proses testing dan meminimalkan duplikasi kode. Penamaan yang konsisten dan dokumentasi singkat per fungsi juga sangat membantu.

6. **Dalam implementasi `MyPaymentService`, langkah tambahan apa yang perlu dilakukan untuk menangani proses pembayaran yang lebih kompleks?**
Kita bisa menambahkan validasi input, integrasi dengan penyedia pembayaran pihak ketiga, serta logging untuk audit. Selain itu, penting juga untuk menambahkan fitur pengecekan saldo, retry saat gagal, dan pengamanan dari transaksi duplikat atau curang.

7. **Apa dampak dari penggunaan gRPC terhadap desain sistem terdistribusi secara keseluruhan?**
gRPC membuat komunikasi antar layanan lebih efisien dan konsisten berkat penggunaan Protobuf. Ini sangat membantu dalam sistem yang terdiri dari banyak microservice. Namun, adopsinya juga menuntut pemahaman tentang tooling dan manajemen schema agar tetap sinkron antar tim atau bahasa pemrograman berbeda.

8. **Apa kelebihan dan kekurangan HTTP/2 sebagai protokol dasar gRPC dibandingkan HTTP/1.1 atau WebSocket pada REST API?**
HTTP/2 memungkinkan beberapa stream dalam satu koneksi, sehingga lebih efisien untuk komunikasi real-time. Ini menjadi keunggulan besar dibandingkan HTTP/1.1 yang harus membuka koneksi baru tiap permintaan. WebSocket juga mendukung real-time, tapi tidak punya struktur sebaik gRPC dan lebih sulit untuk ditangani secara terstandarisasi.

9. **Bagaimana perbandingan model request-response REST API dengan gRPC dalam konteks komunikasi real-time?**
REST API terbatas pada model satu permintaan-satu jawaban, sehingga kurang cocok untuk aplikasi yang butuh komunikasi terus-menerus. gRPC dengan streaming-nya lebih unggul untuk skenario real-time karena lebih ringan dan tidak perlu terus-menerus membuka koneksi baru.

10. **Apa implikasi dari pendekatan schema-based gRPC dibandingkan JSON yang lebih fleksibel?**
 Pendekatan schema-based dengan Protobuf membuat sistem lebih ketat dan terstruktur, sehingga minim risiko error akibat struktur data yang tidak konsisten. Namun, ini juga berarti kita harus lebih disiplin dalam manajemen schema. Sementara JSON lebih fleksibel tapi rentan error, apalagi jika dokumen besar dan tidak tervalidasi dengan baik.
