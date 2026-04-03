# 🎨 AI Image Generator Workflow via n8n

## 📌 Deskripsi Singkat
Repository ini berisi file ekspor workflow JSON untuk otomatisasi pembuatan gambar menggunakan AI (KIE AI API). Sistem ini dibangun menggunakan **n8n** dengan menerapkan arsitektur *polling loop asynchronous*, di mana workflow akan mengirimkan perintah teks (*prompt*), mengecek status pemrosesan secara berkala, dan mengirimkan hasil akhir gambar langsung ke pengguna melalui bot Telegram.

Tugas ini disusun sebagai bagian dari pemenuhan Tugas 2 Implementasi AI Image Generator.

## ✨ Fitur Utama
- **Form Trigger:** Input *prompt*, API Key, dan Chat ID Telegram secara dinamis melalui UI Form.
- **API Integration:** Terhubung langsung dengan *endpoint* Text-to-Image AI.
- **Smart Polling Loop:** Menggunakan kombinasi node `Wait` dan `HTTP Request` untuk mengecek status *generate* gambar setiap 10 detik tanpa membebani server.
- **JSON Parsing:** Mengekstrak URL gambar yang valid dari struktur JSON yang kompleks secara otomatis.
- **Auto-Delivery:** Mengunduh dan mengirimkan gambar (*binary file*) ke pengguna via Telegram.

## 🛠️ Prasyarat (Prerequisites)
Untuk menjalankan workflow ini di *instance* n8n Anda, pastikan Anda memiliki:
1. Akses ke [n8n](https://n8n.io/) (versi Self-Hosted atau Cloud).
2. Kredensial API Key yang valid dari layanan AI penyedia (misal: KIE AI).
3. Bot Telegram aktif dan Chat ID pengguna untuk menerima gambar.

## 🚀 Cara Instalasi & Penggunaan
1. Unduh atau *clone* repository ini.
2. Buka aplikasi n8n Anda.
3. Buat Workflow baru.
4. Di pojok kanan atas, klik menu options (titik tiga) lalu pilih **Import from File**.
5. Pilih file `Asa_Image_Generated.json` dari repository ini.
6. Sesuaikan konfigurasi *Credentials* pada node Telegram Anda.
7. Klik **Test URL** pada node *Form Trigger* untuk mulai mencoba *generate* gambar!

## 🔄 Alur Kerja (Workflow Architecture)
1. **Form Trigger:** Menerima input dari pengguna.
2. **HTTP Request (POST):** Mengirim *prompt* ke AI dan menerima `taskId`.
3. **HTTP Request (GET) & Wait:** Looping setiap 10 detik untuk mengecek status `taskId`.
4. **IF Node:** Memvalidasi apakah status API mengembalikan nilai `success`.
5. **Code Node (JavaScript):** Memecah array URL hasil gambar dari AI.
6. **HTTP Request (GET Binary):** Mengunduh gambar dari URL ke format *binary*.
7. **Telegram Node:** Mengirimkan foto tersebut ke *chat* Telegram yang dituju.

---
*Dibuat oleh [Nama/Username GitHub Kamu] untuk Tugas Eksekusi Workflow n8n.*
