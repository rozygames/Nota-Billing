<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rozy Games - Billing System Mobile</title>
    <!-- Memanggil FontAwesome Online untuk Ikon Sosial Media Resmi -->
    <link rel="stylesheet" href="https://cloudflare.com">
    <style>
        :root {
            --primary-color: #e52d27; 
            --dark-color: #1e1e24;
            --light-bg: #111;
        }
        * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
        
        body { 
            background-color: var(--light-bg);
            color: #333; 
            padding: 15px; 
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        
        .container { 
            width: 100%;
            max-width: 480px; 
            margin: 0 auto; 
            background: rgba(255, 255, 255, 0.96); 
            backdrop-filter: blur(10px); 
            padding: 22px; 
            border-radius: 16px; 
            box-shadow: 0 10px 40px rgba(0,0,0,0.5); 
            position: relative;
            overflow: hidden;
        }

        /* Watermark Logo Rozy Games di Tengah Latar Belakang Kontainer */
        .container::before {
            content: "";
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 320px;
            height: 320px;
            background-image: url('https://googleusercontent.com');
            background-size: contain;
            background-repeat: no-repeat;
            background-position: center;
            opacity: 0.07; 
            pointer-events: none;
            z-index: 0;
        }
        
        /* Lapisan Elemen Utama Berada di Atas Watermark */
        .header, .form-group, .total-box, .btn, .footer-contacts {
            position: relative;
            z-index: 1;
        }
        
        .header { text-align: center; margin-bottom: 20px; border-bottom: 2px dashed #ddd; padding-bottom: 15px; }
        .logo-container { margin-bottom: 10px; }
        .logo-img { width: 110px; height: auto; border-radius: 50%; background: #fff; padding: 3px; box-shadow: 0 4px 12px rgba(0,0,0,0.15); }
        .header h1 { font-size: 24px; color: var(--primary-color); font-weight: 800; letter-spacing: 1px; }
        .header p { font-size: 12px; color: #555; margin-top: 3px; }
        
        .form-group { margin-bottom: 15px; }
        .form-group label { display: block; font-weight: bold; margin-bottom: 5px; font-size: 14px; color: #222; }
        .form-control { width: 100%; padding: 11px; border: 1px solid #ccc; border-radius: 8px; font-size: 14px; background: rgba(255, 255, 255, 0.95); color: #333; }
        .service-row { display: flex; flex-direction: column; background: rgba(245, 245, 245, 0.95); padding: 12px; border: 1px solid #dcdcdc; border-radius: 10px; margin-bottom: 12px; gap: 8px; }
        .row-inputs { display: flex; gap: 10px; }
        .row-inputs select { flex: 2; font-weight: 500; }
        .row-inputs input.qty { flex: 0.6; text-align: center; font-weight: bold; }
        .custom-note { font-size: 13px; padding: 8px; border: 1px solid #ddd; border-radius: 6px; background: #fff; }
        
        .btn { display: block; width: 100%; padding: 12px; background: var(--primary-color); color: #fff; border: none; border-radius: 8px; font-size: 16px; font-weight: bold; cursor: pointer; margin-top: 15px; text-align: center; text-decoration: none; transition: background 0.2s; box-shadow: 0 4px 10px rgba(229, 45, 39, 0.3); }
        .btn:hover { background: #b81d18; }
        .btn-add { background: #28a745; margin-bottom: 15px; font-size: 14px; padding: 8px; box-shadow: 0 3px 6px rgba(40, 167, 69, 0.2); }
        .btn-add:hover { background: #218838; }
        
        .total-box { background: var(--dark-color); color: #fff; padding: 15px; border-radius: 8px; text-align: right; margin-top: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.25); }
        .total-box p { font-size: 13px; opacity: 0.8; }
        .total-box h2 { font-size: 22px; color: #ffc107; font-weight: bold; margin-top: 2px; }
        .note-bensin { font-size: 11px; color: #c9302c; font-style: italic; margin-top: 4px; display: block; font-weight: 500; }
        optgroup { font-weight: bold; background: #f1f1f1; }

        /* Media Sosial Footer Berlogo Asli */
        .footer-contacts { margin-top: 25px; padding-top: 15px; border-top: 2px dashed #ddd; text-align: center; font-size: 12px; color: #333; }
        .contact-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 8px; margin-top: 10px; }
        .contact-item { display: flex; align-items: center; justify-content: flex-start; gap: 8px; background: rgba(0, 0, 0, 0.04); padding: 8px 12px; border-radius: 6px; font-weight: 600; }
        
        .contact-item i.fa-whatsapp { color: #25D366; font-size: 14px; }
        .contact-item i.fa-youtube { color: #FF0000; font-size: 14px; }
        .contact-item i.fa-instagram { color: #E1306C; font-size: 14px; }
        .contact-item i.fa-tiktok { color: #000000; font-size: 14px; }
        
        /* Pengaturan Cetak/Simpan PDF Kertas Bersih */
        @media print {
            body { background: #fff !important; padding: 0; }
            .container { box-shadow: none; max-width: 100%; padding: 0; background: #fff !important; }
            .container::before { opacity: 0.04; } 
            .no-print { display: none; }
            .logo-img { box-shadow: none; width: 90px; }
            .total-box { background: #eee !important; color: #000 !important; }
            .total-box h2 { color: #000 !important; }
            .service-row { border: none; padding: 5px 0; margin-bottom: 5px; background: none !important; }
            .contact-item { background: none; border: 1px solid #eee; }
        }
    </style>
</head>
<body>

<div class="container">
    <!-- Bagian Kepala Toko -->
    <div class="header">
        <div class="logo-container">
            <img src="https://googleusercontent.com" alt="Logo Rozy Games" class="logo-img" onerror="this.src='https://placehold.co'">
        </div>
        <h1>ROZY GAMES</h1>
        <p>Spesialis Isi Game PS3, PS4 HEN, & PS5 HEN Terlengkap</p>
        <p>Kota Solok, Sumatera Barat</p>
    </div>

    <!-- Data Pembeli -->
    <div class="form-group">
        <label>Nama Pelanggan</label>
        <input type="text" id="customerName" class="form-control" placeholder="Nama pembeli...">
    </div>
    <div class="form-group">
        <label>Tanggal Transaksi</label>
        <input type="date" id="invoiceDate" class="form-control">
    </div>

    <!-- Pilihan Layanan -->
    <div class="form-group">
        <label>Daftar Layanan / Game</label>
        <div id="servicesContainer">
            <!-- Baris item akan dimasukkan otomatis oleh JS -->
        </div>
        <button type="button" class="btn btn-add no-print" onclick="addServiceRow()">+ Tambah Item</button>
    </div>

    <!-- Ongkos Kirim / Bensin -->
    <div class="form-group">
        <label>Uang Bensin Antar Alamat (Rp)</label>
        <input type="number" id="extraFee" class="form-control" value="0" oninput="calculateTotal()">
        <span class="note-bensin">*Bantu bensin disesuaikan berdasarkan jarak alamat.</span>
    </div>

    <!-- Kalkulasi Angka Akhir -->
    <div class="total-box">
        <p>Total Pembayaran:</p>
        <h2 id="totalDisplay">Rp 0</h2>
    </div>

    <!-- Cetak Dokumen Nota -->
    <button class="btn no-print" onclick="window.print()">Cetak / Simpan PDF</button>

    <!-- Informasi Kontak Lengkap Sosmed -->
    <div class="footer-contacts">
        <p><strong>Hubungi Kami Kembali:</strong></p>
        <div class="contact-grid">
            <div class="contact-item"><i class="fa-brands fa-whatsapp"></i> 0812 7063 5111</div>
            <div class="contact-item"><i class="fa-brands fa-youtube"></i> Rozy Games</div>
            <div class="contact-item"><i class="fa-brands fa-instagram"></i> Rozy Games</div>
            <div class="contact-item"><i class="fa-brands fa-tiktok"></i> Rozy Games</div>
        </div>
    </div>
</div>

<script>
    // Ambil tanggal hari ini secara otomatis
    document.getElementById('invoiceDate').value = new Date().toISOString().substring(0, 10);

    // Database Master Tarif Resmi Rozy Games
    const menuStructure = [
        {
            groupName: "PATCH BOLA (FREE UPDATE S/D AKHIR MUSIM)",
            options: [
                { name: "Bitbox Patch PS3", price: 20000 },
                { name: "Gembox Patch PS3", price: 20000 },
                { name: "VR Patch PS3", price: 20000 },
                { name: "Bitbox Patch PS4 HEN", price: 50000 },
                { name: "Monster Patch PS4 HEN", price: 50000 }
            ]
        },
        {
            groupName: "ISI GAME SATUAN (SELAIN BOLA)",
            options: [
                { name: "Isi Game PS3 (Per Game)", price: 10000 },
                { name: "Isi Game PS4 HEN (Per Game)", price: 25000 }
            ]
        },
        {
            groupName: "PAKET HEMAT FULL GAME PS3",
            options: [
                { name: "Paket Full Game PS3 160GB", price: 100000 },
                { name: "Paket Full Game PS3 250GB", price: 120000 },
                { name: "Paket Full Game PS3 320GB", price: 150000 },
                { name: "Paket Full Game PS3 500GB", price: 200000 }
            ]
        },
        {
            groupName: "PAKET HEMAT FULL GAME PS4",
            options: [
                { name: "Paket Full Game PS4 500GB", price: 150000 },
                { name: "Paket Full Game PS4 1TB", price: 200000 },
