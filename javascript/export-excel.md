# Mengekspor Tabel HTML ke Excel

### Langkah 1: Sertakan Library `SheetJS`

Tambahkan skrip `SheetJS` ke HTML Anda:
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
```

### Langkah 2: Buat Tombol dan Tabel HTML

Berikut adalah struktur HTML untuk tabel dan tombol ekspor:
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Export Tabel HTML</title>
</head>
<body>
    <table id="table1" border="1">
        <thead>
            <tr>
                <th>Nama Anak</th>
                <th>Tanggal Penimbangan</th>
                <th>Penimbangan Bulan Lalu</th>
                <th>Penimbangan Sekarang</th>
                <th>Tinggi Badan</th>
                <th>Status Penimbangan</th>
                <th>Aksi</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Alice</td>
                <td>2024-08-10</td>
                <td>15 kg</td>
                <td>16 kg</td>
                <td>100 cm</td>
                <td>Normal</td>
                <td>Edit | Hapus</td>
            </tr>
            <!-- Baris lainnya -->
        </tbody>
    </table>
    <button id="btnExcel" class="btn btn-success btn-sm" onclick="exportToExcel('table1', 'penimbangan_anak.xlsx')">Excel</button>

    <script>
        function exportToExcel(tableId, fileName) {
            var wb = XLSX.utils.book_new();
            var ws = XLSX.utils.table_to_sheet(document.getElementById(tableId));
            XLSX.utils.book_append_sheet(wb, ws, 'Data');
            XLSX.writeFile(wb, fileName);
        }
    </script>
</body>
</html>
```
