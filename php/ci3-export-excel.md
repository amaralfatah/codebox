# Export Data Menjadi Excel - CodeIgniter 3

Dokumentasi ini menjelaskan langkah-langkah untuk mengekspor data menjadi file Excel menggunakan CodeIgniter 3 dan PhpSpreadsheet.

## Instalasi PhpSpreadsheet

Instal library `phpoffice/phpspreadsheet` menggunakan Composer:

```sh
composer require phpoffice/phpspreadsheet
```

## Konfigurasi Controller

Tambahkan kode berikut di bagian atas file controller Anda untuk mengimpor kelas yang diperlukan dari PhpSpreadsheet:

```php
require 'vendor/autoload.php';

use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
```

### Membuat Fungsi Export

Buat fungsi export di controller Anda untuk mengekspor data ke file Excel:

```php
public function export(){
    $this->load->helper('download');

    // Mengambil data dari model
    $data = $this->M_guest->get_guests();

    if (empty($data)) {
        echo "Tidak ada data untuk diekspor";
        exit;
    }

    $spreadsheet = new Spreadsheet();
    $sheet = $spreadsheet->getActiveSheet();

    // Menambahkan header kolom
    $sheet->setCellValue('A1', 'Nama');
    $sheet->setCellValue('B1', 'Telepon');
    $sheet->setCellValue('C1', 'Keperluan');
    $sheet->setCellValue('D1', 'Tanggal');
    $sheet->setCellValue('E1', 'Status');
    $sheet->setCellValue('F1', 'Instansi/Eksternal');

    // Menambahkan data ke dalam sheet
    $row = 2;
    foreach ($data as $row_data) {
        $sheet->setCellValue('A' . $row, $row_data['nama']);
        $sheet->setCellValue('B' . $row, $row_data['telp']);
        $sheet->setCellValue('C' . $row, $row_data['keperluan']);
        $sheet->setCellValue('D' . $row, $row_data['created_at']);
        $sheet->setCellValue('E' . $row, $row_data['status']);
        $sheet->setCellValue('F' . $row, $row_data['instansi'] ? $row_data['instansi'] : 'Tidak ada');
        $row++;
    }

    // Menyimpan file Excel
    $writer = new Xlsx($spreadsheet);
    $filename = 'data_export.xlsx';
    $writer->save($filename);

    // Memaksa unduhan file
    force_download($filename, NULL);
}
```

<br><br>
syukron --rye
