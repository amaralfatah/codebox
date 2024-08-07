# Export Data Menjadi Excel - Codeigniter 3

install phpoffice/phpspreadsheet

```php
composer require phpoffice/phpspreadsheet
```

letakan diatas controller

```php
require 'vendor/autoload.php';

use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
```

buat fungsi export

```php
public function export(){
    $this->load->helper('download');

    $data = $this->M_guest->get_guests();

    if (empty($data)) {
    echo "Tidak ada data untuk diekspor";
    exit;
    }

    $spreadsheet = new Spreadsheet();
    $sheet = $spreadsheet->getActiveSheet();

    // Header kolom - sesuaikan dengan data yang diperlukan
    $sheet->setCellValue('A1', 'Nama');
    $sheet->setCellValue('B1', 'Telepon');
    $sheet->setCellValue('C1', 'Keperluan');
    $sheet->setCellValue('D1', 'Tanggal');
    $sheet->setCellValue('E1', 'Status');
    $sheet->setCellValue('F1', 'Instansi/Eksternal');

    // Data - sesuaikan dengan data yang diperlukan
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

    $writer = new Xlsx($spreadsheet);
    $filename = 'data_export.xlsx';
    $writer->save($filename);

    force_download($filename, NULL);
}
```

شكرًا --rye
