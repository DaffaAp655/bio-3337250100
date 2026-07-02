# Penjelasan Sintaksis - Pertemuan 4 (Pembaruan Accordion & Tooltip)

Dokumen ini menjelaskan pembaruan sintaksis HTML dan CSS yang digunakan untuk membuat komponen **Accordion Bootstrap** pada bagian Riwayat & Pengalaman, serta **Custom CSS Tooltip** saat daftar keahlian (*skills*) di-hover.

---

## 1. Komponen Accordion Bootstrap 5

Accordion digunakan untuk mengelompokkan informasi besar (seperti Riwayat Pendidikan dan Pengalaman) agar dapat diciutkan/dikembangkan secara interaktif.

```html
<div class="accordion" id="accordionProfile">
    <!-- Item 1 -->
    <div class="accordion-item">
        <h3 class="accordion-header" id="headingPendidikan">
            <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapsePendidikan" aria-expanded="true" aria-controls="collapsePendidikan">
                Riwayat Pendidikan
            </button>
        </h3>
        <div id="collapsePendidikan" class="accordion-collapse collapse show" aria-labelledby="headingPendidikan" data-bs-parent="#accordionProfile">
            <div class="accordion-body">
                <!-- Konten Tabel Pendidikan -->
            </div>
        </div>
    </div>
</div>
```

### Penjelasan Atribut Utama Accordion:
- **`class="accordion"`**: Kelas utama Bootstrap untuk membungkus seluruh item akordion.
- **`data-bs-toggle="collapse"`**: Atribut pemicu JavaScript Bootstrap untuk mengubah status visibilitas konten (sembunyi/tampil).
- **`data-bs-target="#collapsePendidikan"`**: Menentukan elemen target mana yang akan diciutkan/dikembangkan berdasarkan kecocokan ID elemen target (`id="collapsePendidikan"`).
- **`data-bs-parent="#accordionProfile"`**: Mengaitkan semua item ke satu induk akordion. Hal ini memastikan ketika satu item dibuka, item lainnya yang sedang terbuka akan menutup secara otomatis (perilaku eksklusif akordion).
- **`class="accordion-collapse collapse show"`**:
  - `collapse`: Menyembunyikan konten secara default.
  - `show`: Menampilkan konten tersebut secara default saat halaman pertama kali dimuat (diterapkan pada Riwayat Pendidikan).

---

## 2. Kustom CSS Tooltip (Hover Penjelasan Skill)

Menampilkan detail tingkat keahlian (*skill level* seperti Native atau Intermediate) menggunakan CSS murni tanpa membutuhkan JavaScript tambahan.

### Sintaksis HTML:
```html
<span class="skill-item" data-tooltip="Native">Team Working</span>
```
- **`data-tooltip="Native"`**: Sebuah atribut khusus HTML5 (*custom data attribute*) yang menyimpan teks penjelasan level keahlian. Atribut ini nanti akan dibaca oleh CSS.

### Sintaksis CSS:
```css
/* 1. Kontainer Elemen */
.skill-item {
    position: relative;
    cursor: pointer;
}

/* 2. Gelembung Tooltip (Box Atas) */
.skill-item::after {
    content: attr(data-tooltip);
    position: absolute;
    bottom: 130%;
    left: 50%;
    transform: translateX(-50%) scale(0.85);
    background-color: rgba(0, 0, 0, 0.85);
    color: #fff;
    padding: 6px 12px;
    border-radius: 8px;
    font-size: 12px;
    white-space: nowrap;
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.15s ease, transform 0.15s ease, visibility 0.15s ease;
    z-index: 100;
}

/* 3. Segitiga Penunjuk (Arrow) */
.skill-item::before {
    content: "";
    position: absolute;
    bottom: 115%;
    left: 50%;
    transform: translateX(-50%) scale(0.85);
    border-width: 6px 6px 0;
    border-style: solid;
    border-color: rgba(0, 0, 0, 0.85) transparent transparent;
    opacity: 0;
    visibility: hidden;
    transition: opacity 0.15s ease, transform 0.15s ease, visibility 0.15s ease;
    z-index: 100;
}

/* 4. Efek Muncul Saat Hover */
.skill-item:hover::after,
.skill-item:hover::before {
    opacity: 1;
    visibility: visible;
    transform: translateX(-50%) scale(1);
}
```
- **`::after` dan `::before`**: *Pseudo-elements* yang digunakan untuk menyisipkan elemen dekoratif buatan di awal/akhir konten elemen utama tanpa mengubah DOM HTML.
- **`content: attr(data-tooltip)`**: Fungsi CSS untuk mengambil string teks dari atribut `data-tooltip="..."` pada tag HTML dan merendernya sebagai konten teks tooltip.
- **`transition` & `transform: scale(...)`**: Memberikan animasi transisi pemesaran halus (*micro-animation*) saat tooltip muncul.
- **`pointer-events: none`**: Mencegah tooltip menangkap interaksi kursor mouse agar tidak mengganggu klik pada tombol/tautan di bawahnya.

---

## 3. Gaya Tabel Terpadu (Bootstrap Table Classes)

Tabel di dalam akordion menggunakan utilitas kelas tabel Bootstrap untuk meningkatkan estetika:
- **`table`**: Memberikan gaya dasar tabel Bootstrap (garis batas bawah, jarak baris yang rapi).
- **`table-striped`**: Memberikan warna belang-selang abu-abu muda pada baris genap untuk memudahkan pembacaan data baris.
- **`table-hover`**: Memberikan efek perubahan warna latar belakang baris (*highlight*) saat kursor mouse digeser di atasnya.
- **`mb-0`**: Menghilangkan margin bawah tabel bawaan Bootstrap (`margin-bottom: 0`) agar pas berada di dalam akordion tanpa menyisakan ruang kosong yang tidak perlu.

---

## 4. Integrasi Bootstrap JavaScript Bundle

Agar aksi klik akordion dapat membuka dan menutup dengan animasi runtuh (*collapse*), berkas JavaScript Bootstrap dimasukkan di akhir dokumen sebelum penutupan tag `</body>`:
```html
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
```
