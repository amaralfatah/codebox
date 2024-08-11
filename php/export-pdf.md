# Mengekspor Tabel HTML ke Pdf

### Langkah 1: Sertakan Library jsPDF dan autoTable

Tambahkan skrip jsPDF dan autoTable ke HTML Anda:
```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.3.1/jspdf.umd.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf-autotable/3.5.22/jspdf.plugin.autotable.min.js"></script>
```

### Langkah 2: Buat Tombol dan Tabel HTML

Tambahkan tombol dan tabel HTML yang sama dengan yang kita gunakan untuk Excel:
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
    <button id="btnPdf">Export to PDF</button>

    <script>
        document.getElementById('btnPdf').addEventListener('click', function() {
            const { jsPDF } = window.jspdf;
            var doc = new jsPDF();
            var table = document.getElementById('table1');
            var rows = [];
            
            // Extract table data
            for (var i = 1; i < table.rows.length; i++) { // start at 1 to skip header row
                var row = [];
                for (var j = 0; j < table.rows[i].cells.length; j++) {
                    row.push(table.rows[i].cells[j].innerText); // Use innerText to get clean text
                }
                rows.push(row);
            }

            // Add table to PDF
            doc.autoTable({
                head: [['Nama Anak', 'Tanggal Penimbangan', 'Penimbangan Bulan Lalu', 'Penimbangan Sekarang', 'Tinggi Badan', 'Status Penimbangan', 'Aksi']],
                body: rows,
                theme: 'grid',
                styles: {
                    fontSize: 10,
                    fontStyle: 'normal',
                    overflow: 'linebreak',
                    columnWidth: 'auto'
                }
            });

            doc.save('penimbangan_anak.pdf');
        });
    </script>
</body>
</html>
```
