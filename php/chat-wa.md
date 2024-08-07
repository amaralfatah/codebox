# Kirim Pesan WhatsApp

Dokumentasi ini menjelaskan cara membuat fungsi untuk menangani format nomor telepon, mengatur link WhatsApp, dan membuat trigger untuk mengirim pesan melalui WhatsApp.

## Steps

1. Fungsi untuk menangani berbagai format penulisan nomor telepon dan mengonversinya ke format internasional (+62 untuk Indonesia):
    ```php
    function hp($string) {
        // Menghapus spasi, tanda kurung, dan titik dari nomor telepon
        $string = str_replace([" ", "(", ")", "."], "", $string);
    
        // Memeriksa apakah nomor telepon hanya mengandung karakter yang valid (+ dan 0-9)
        if (!preg_match('/[^+0-9]/', trim($string))) {
            if (substr(trim($string), 0, 3) == '+62') {
                // Jika nomor telepon sudah dalam format internasional (+62)
                $string = trim($string);
            } elseif (substr(trim($string), 0, 1) == '0') {
                // Jika nomor telepon dimulai dengan '0', ganti dengan '+62'
                $string = '+62' . substr(trim($string), 1);
            }
        } else {
            // Jika nomor telepon tidak valid
            $string = 'Format nomor telepon yang dimasukkan tidak lengkap atau salah!';
        }
    
        return $string;
    }
    ```

2. Mengatur Link WhatsApp:
    ```php
    $nohp = hp($guest['telp']);
    $message = '&text=' . urlencode('Halo! layanan anda sedang kami proses');
    
    // Menentukan link WhatsApp berdasarkan jenis perangkat (mobile atau desktop)
    $linkwa = $this->agent->is_mobile()
        ? 'https://api.whatsapp.com/send?phone=' . $nohp . $message
        : 'whatsapp://send?phone=' . $nohp . $message;
    ```

3. Membuat Trigger
    ```php
    <a href="<?= $linkwa ?>">ChatWA</a>
    ```

<br><br>
syukron --rye
