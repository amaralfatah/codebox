# Kirim Pesan WhatsApp

Dokumentasi ini menjelaskan cara membuat fungsi untuk menangani format nomor telepon, mengatur link WhatsApp, dan membuat trigger untuk mengirim pesan melalui WhatsApp.

## Steps

1. Fungsi untuk menangani berbagai format penulisan nomor telepon dan mengonversinya ke format internasional (+62 untuk Indonesia)
    ```php
    function hp($string) {
        $string = str_replace([" ", "(", ")", "."], "", $string);
        if (!preg_match('/[^+0-9]/', trim($string))) {
            if (substr(trim($string), 0, 3) == '+62') {
                $string = trim($string);
            } elseif (substr(trim($string), 0, 1) == '0') {
                $string = '+62' . substr(trim($string), 1);
            }
        } else {
            $string = 'Format nomor telepon yang dimasukkan tidak lengkap atau salah!';
        }
        return $string;
    }
    ```

2. Mengatur Link WhatsApp
    ```php
    $nohp = hp($telp);
    $message = '&text=' . urlencode('Halo! layanan anda sedang kami proses');
    $linkwa = $this->agent->is_mobile()
        ? 'https://api.whatsapp.com/send?phone=' . $nohp . $message
        : 'whatsapp://send?phone=' . $nohp . $message;
    ```

3. Membuat Trigger
    ```html
    <a href="<?= $linkwa ?>">ChatWA</a>
    ```

<br><br>
syukron --rye
