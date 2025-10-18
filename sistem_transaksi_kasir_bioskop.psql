-- Database Cinema Ticketing System
-- PostgreSQL Script

-- Drop tables if exists
DROP TABLE IF EXISTS tiket CASCADE;
DROP TABLE IF EXISTS transaksi CASCADE;
DROP TABLE IF EXISTS jadwal CASCADE;
DROP TABLE IF EXISTS studio CASCADE;
DROP TABLE IF EXISTS film CASCADE;
DROP TABLE IF EXISTS kasir CASCADE;
DROP TABLE IF EXISTS pelanggan CASCADE;

-- Create Tables
CREATE TABLE pelanggan (
    id_pelanggan SERIAL PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    nomor_telepon VARCHAR(20)
);

CREATE TABLE kasir (
    id_kasir SERIAL PRIMARY KEY,
    nama VARCHAR(100) NOT NULL,
    shift_kerja VARCHAR(20) NOT NULL
);

CREATE TABLE film (
    id_film SERIAL PRIMARY KEY,
    judul VARCHAR(200) NOT NULL,
    genre VARCHAR(50) NOT NULL,
    durasi INTEGER NOT NULL,
    rating DECIMAL(3,1)
);

CREATE TABLE studio (
    id_studio SERIAL PRIMARY KEY,
    nama_studio VARCHAR(50) NOT NULL,
    kapasitas INTEGER NOT NULL
);

CREATE TABLE jadwal (
    id_jadwal SERIAL PRIMARY KEY,
    id_film INTEGER REFERENCES film(id_film),
    id_studio INTEGER REFERENCES studio(id_studio),
    tanggal DATE NOT NULL,
    jam_tayang TIME NOT NULL
);

CREATE TABLE transaksi (
    id_transaksi SERIAL PRIMARY KEY,
    id_pelanggan INTEGER REFERENCES pelanggan(id_pelanggan),
    id_kasir INTEGER REFERENCES kasir(id_kasir),
    total_harga DECIMAL(10,2) NOT NULL,
    tanggal_transaksi TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE tiket (
    id_tiket SERIAL PRIMARY KEY,
    id_transaksi INTEGER REFERENCES transaksi(id_transaksi),
    id_jadwal INTEGER REFERENCES jadwal(id_jadwal),
    nomor_kursi VARCHAR(10) NOT NULL,
    harga_film DECIMAL(10,2) NOT NULL
);

-- Insert Data Pelanggan (1000 records)
INSERT INTO pelanggan (nama, email, nomor_telepon) VALUES
('Budi Santoso', 'budi.santoso@email.com', '081234567890'),
('Siti Nurhaliza', 'siti.nurhaliza@email.com', '082345678901'),
('Ahmad Wijaya', 'ahmad.wijaya@email.com', '083456789012'),
('Dewi Lestari', 'dewi.lestari@email.com', '084567890123'),
('Rudi Hartono', 'rudi.hartono@email.com', '085678901234'),
('Maya Sari', 'maya.sari@email.com', '086789012345'),
('Eko Prasetyo', 'eko.prasetyo@email.com', '087890123456'),
('Nina Kartika', 'nina.kartika@email.com', '088901234567'),
('Fajar Ramadhan', 'fajar.ramadhan@email.com', '089012345678'),
('Linda Permata', 'linda.permata@email.com', '081123456789'),
('Hendra Gunawan', 'hendra.gunawan@email.com', '082234567890'),
('Ratna Sari', 'ratna.sari@email.com', '083345678901'),
('Doni Setiawan', 'doni.setiawan@email.com', '084456789012'),
('Indah Kusuma', 'indah.kusuma@email.com', '085567890123'),
('Andi Saputra', 'andi.saputra@email.com', '086678901234'),
('Fitri Handayani', 'fitri.handayani@email.com', '087789012345'),
('Agus Salim', 'agus.salim@email.com', '088890123456'),
('Diana Putri', 'diana.putri@email.com', '089901234567'),
('Bambang Sutopo', 'bambang.sutopo@email.com', '081234567891'),
('Sri Wahyuni', 'sri.wahyuni@email.com', '082345678902');

-- Generate remaining 980 pelanggan records
DO $$
DECLARE
    i INTEGER;
    nama_depan TEXT[] := ARRAY['Agus', 'Budi', 'Citra', 'Dewi', 'Eko', 'Fitri', 'Gilang', 'Hana', 'Indra', 'Joko', 
                               'Kartika', 'Lina', 'Made', 'Nisa', 'Omar', 'Putri', 'Qori', 'Rina', 'Sari', 'Tono',
                               'Umar', 'Vina', 'Wati', 'Yanto', 'Zahra', 'Adi', 'Bella', 'Candra', 'Dina', 'Erik'];
    nama_belakang TEXT[] := ARRAY['Santoso', 'Wijaya', 'Permata', 'Kusuma', 'Pratama', 'Lestari', 'Saputra', 'Handayani', 
                                  'Gunawan', 'Setiawan', 'Hartono', 'Ramadhan', 'Kartika', 'Salim', 'Sutopo', 'Wahyuni',
                                  'Prasetyo', 'Nurhaliza', 'Saragih', 'Hakim', 'Rahman', 'Hidayat', 'Nugraha', 'Susanto',
                                  'Firmansyah', 'Kurniawan', 'Wibowo', 'Irawan', 'Mahendra', 'Putra'];
BEGIN
    FOR i IN 21..1000 LOOP
        INSERT INTO pelanggan (nama, email, nomor_telepon)
        VALUES (
            nama_depan[1 + floor(random() * 30)::int] || ' ' || nama_belakang[1 + floor(random() * 30)::int],
            'pelanggan' || i || '@email.com',
            '08' || LPAD((1000000000 + floor(random() * 900000000))::TEXT, 10, '0')
        );
    END LOOP;
END $$;

-- Insert Data Kasir (10 records)
INSERT INTO kasir (nama, shift_kerja) VALUES
('Rina Wulandari', 'Pagi'),
('Dimas Prasetyo', 'Siang'),
('Ayu Lestari', 'Malam'),
('Bagus Setiawan', 'Pagi'),
('Clara Wijaya', 'Siang'),
('Farid Rahman', 'Malam'),
('Gita Permatasari', 'Pagi'),
('Hadi Nugroho', 'Siang'),
('Intan Kartika', 'Malam'),
('Johan Saputra', 'Pagi');

-- Insert Data Film (100 records)
INSERT INTO film (judul, genre, durasi, rating) VALUES
('Pengabdi Setan 2', 'Horror', 119, 7.2),
('KKN di Desa Penari', 'Horror', 175, 6.8),
('Miracle in Cell No. 7', 'Drama', 145, 8.5),
('Dilan 1990', 'Romance', 110, 7.9),
('Si Doel The Movie', 'Comedy', 108, 6.5),
('Laskar Pelangi', 'Drama', 125, 8.0),
('Habibie & Ainun', 'Biography', 120, 7.8),
('My Stupid Boss', 'Comedy', 106, 6.3),
('Perahu Kertas', 'Romance', 110, 7.1),
('Filosofi Kopi', 'Drama', 117, 7.4),
('The Raid', 'Action', 101, 8.5),
('Jailangkung', 'Horror', 95, 6.0),
('Keluarga Cemara', 'Drama', 110, 8.2),
('Ada Apa Dengan Cinta', 'Romance', 112, 7.8),
('Petualangan Sherina', 'Adventure', 114, 7.5),
('Ayat-Ayat Cinta', 'Romance', 120, 7.2),
('Warkop DKI Reborn', 'Comedy', 102, 6.8),
('Critical Eleven', 'Romance', 118, 7.0),
('Surat dari Praha', 'Drama', 103, 6.9),
('Danur', 'Horror', 92, 6.4);

-- Generate remaining 80 film records
DO $$
DECLARE
    i INTEGER;
    judul_prefix TEXT[] := ARRAY['Kisah', 'Petualangan', 'Cinta', 'Legenda', 'Misteri', 'Rahasia', 'Keajaiban', 
                                 'Perjalanan', 'Takdir', 'Mimpi', 'Jejak', 'Bayangan', 'Cahaya', 'Gelap', 'Terang'];
    genre_list TEXT[] := ARRAY['Horror', 'Drama', 'Comedy', 'Romance', 'Action', 'Adventure', 'Thriller'];
BEGIN
    FOR i IN 21..100 LOOP
        INSERT INTO film (judul, genre, durasi, rating)
        VALUES (
            judul_prefix[1 + floor(random() * 15)::int] || ' ' || (2020 + floor(random() * 6)::int)::TEXT,
            genre_list[1 + floor(random() * 7)::int],
            90 + floor(random() * 90)::int,
            5.0 + (random() * 4)::NUMERIC(3,1)
        );
    END LOOP;
END $$;

-- Insert Data Studio (10 records)
INSERT INTO studio (nama_studio, kapasitas) VALUES
('Studio 1', 150),
('Studio 2', 120),
('Studio 3', 100),
('Studio 4', 180),
('Studio 5', 130),
('Studio VIP 1', 50),
('Studio VIP 2', 40),
('Studio IMAX', 200),
('Studio 3D-1', 140),
('Studio Premier', 80);

-- Insert Data Jadwal (1000 records)
DO $$
DECLARE
    i INTEGER;
    tanggal_mulai DATE := '2025-01-01';
    jam_list TIME[] := ARRAY['10:00', '12:30', '15:00', '17:30', '20:00', '22:30'];
BEGIN
    FOR i IN 1..1000 LOOP
        INSERT INTO jadwal (id_film, id_studio, tanggal, jam_tayang)
        VALUES (
            1 + floor(random() * 100)::int,
            1 + floor(random() * 10)::int,
            tanggal_mulai + floor(random() * 90)::int,
            jam_list[1 + floor(random() * 6)::int]
        );
    END LOOP;
END $$;

-- Insert Data Transaksi (10000 records)
DO $$
DECLARE
    i INTEGER;
    jumlah_tiket INTEGER;
    harga_per_tiket DECIMAL(10,2);
    total DECIMAL(10,2);
BEGIN
    FOR i IN 1..10000 LOOP
        jumlah_tiket := 1 + floor(random() * 4)::int; -- 1-4 tiket per transaksi
        harga_per_tiket := 35000 + (floor(random() * 6)::int * 10000); -- 35k - 85k
        total := jumlah_tiket * harga_per_tiket;
        
        INSERT INTO transaksi (id_pelanggan, id_kasir, total_harga, tanggal_transaksi)
        VALUES (
            1 + floor(random() * 1000)::int,
            1 + floor(random() * 10)::int,
            total,
            TIMESTAMP '2025-01-01 00:00:00' + 
            (floor(random() * 90) || ' days')::INTERVAL + 
            (floor(random() * 14) || ' hours')::INTERVAL +
            (floor(random() * 60) || ' minutes')::INTERVAL
        );
    END LOOP;
END $$;

-- Insert Data Tiket (10000 records)
DO $$
DECLARE
    i INTEGER;
    huruf CHAR[] := ARRAY['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J'];
    harga DECIMAL(10,2);
BEGIN
    FOR i IN 1..10000 LOOP
        -- Harga tiket bervariasi: Reguler 35k-45k, VIP 75k-85k
        IF random() < 0.2 THEN
            harga := 75000 + (floor(random() * 2)::int * 5000);
        ELSE
            harga := 35000 + (floor(random() * 3)::int * 5000);
        END IF;
        
        INSERT INTO tiket (id_transaksi, id_jadwal, nomor_kursi, harga_film)
        VALUES (
            i,
            1 + floor(random() * 1000)::int,
            huruf[1 + floor(random() * 10)::int] || (1 + floor(random() * 20)::int)::TEXT,
            harga
        );
    END LOOP;
END $$;

-- Indexes untuk performa query
CREATE INDEX idx_jadwal_film ON jadwal(id_film);
CREATE INDEX idx_jadwal_studio ON jadwal(id_studio);
CREATE INDEX idx_jadwal_tanggal ON jadwal(tanggal);
CREATE INDEX idx_transaksi_pelanggan ON transaksi(id_pelanggan);
CREATE INDEX idx_transaksi_tanggal ON transaksi(tanggal_transaksi);
CREATE INDEX idx_tiket_transaksi ON tiket(id_transaksi);
CREATE INDEX idx_tiket_jadwal ON tiket(id_jadwal);

-- Query untuk verifikasi jumlah data
SELECT 
    'pelanggan' as tabel, COUNT(*) as jumlah_baris FROM pelanggan
UNION ALL
SELECT 'kasir', COUNT(*) FROM kasir
UNION ALL
SELECT 'film', COUNT(*) FROM film
UNION ALL
SELECT 'studio', COUNT(*) FROM studio
UNION ALL
SELECT 'jadwal', COUNT(*) FROM jadwal
UNION ALL
SELECT 'transaksi', COUNT(*) FROM transaksi
UNION ALL
SELECT 'tiket', COUNT(*) FROM tiket
ORDER BY tabel;
