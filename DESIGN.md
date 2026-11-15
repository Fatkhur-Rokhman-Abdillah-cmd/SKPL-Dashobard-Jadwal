# DESIGN SYSTEM & UI GUIDELINES (`DESIGN.md`)
## SISTEM DATA JADWAL KULIAH (CLASS SCHEDULE)

---

### Dokumen Kontrol
- **Nama Dokumen:** Design System & UI Guidelines
- **Versi:** 1.0.0
- **Status:** Approved / Acuan Mutlak Pengembangan Frontend AI di VS Code
- **Framework UI:** Tailwind CSS (v3+)
- **Font Stack:** Inter / Plus Jakarta Sans

---

## 1. PALET WARNA TAILWIND CSS (COLOR PALETTE)

Sistem menggunakan palet warna standar berbasis Tailwind CSS untuk menciptakan antarmuka yang bersih, modern, profesional, dan memiliki kontras yang ramah mata (*accessible*).

### 1.1 Warna Inti Sistem (*Core Theme Colors*)

| Peran Warna | Tailwind Class | Nilai HEX | Penggunaan & Penerapan |
| :--- | :--- | :--- | :--- |
| **Main Background** | `bg-slate-50` | `#F8FAFC` | Latar belakang kanvas aplikasi secara menyeluruh (`body` / *root layout*). |
| **Card / Surface** | `bg-white` | `#FFFFFF` | Kontainer kartu metrik, form panel, modal dialog, dan tabel data. |
| **Border / Divider** | `border-slate-200` | `#E2E8F0` | Garis tepi (*border*) kartu, batas baris tabel (*divide-y*), dan garis pemisah. |
| **Primary Color** | `bg-indigo-600` / `text-indigo-600` | `#4F46E5` | Tombol aksi utama (*Add/Submit*), tautan aktif, fokus input ring, dan *brand icon*. |
| **Primary Hover/Active** | `hover:bg-indigo-700` | `#4338CA` | State interaktif ketika tombol primer di-*hover* atau di-*click*. |
| **Success / Masuk** | `bg-emerald-600` / `text-emerald-600` | `#059669` | Toast notifikasi sukses, badge jadwal valid/aktif, status berhasil disimpan. |
| **Success Subtle** | `bg-emerald-50` / `border-emerald-200` | `#ECFDF5` | Latar badge sukses dan banner feedback keberhasilan operasi CRUD. |
| **Danger / Error** | `bg-rose-600` / `text-rose-600` | `#E11D48` | Tombol hapus (*destructive*), validasi bentrok gagal (`TC-01`), teks error input. |
| **Danger Subtle** | `bg-rose-50` / `border-rose-200` | `#FFF1F2` | Latar *alert banner* saat bentrok terdeteksi (`TC-01`) dan modal konfirmasi hapus. |
| **Warning / Warning** | `bg-amber-500` / `text-amber-500` | `#F59E0B` | Peringatan perubahan data, status waktu menjelang pergantian jam kuliah. |

### 1.2 Skala Warna Teks & Tipografi (*Text Colors*)
* **Heading / Teks Utama:** `text-slate-900` (`#0F172A`) — Judul halaman, nama mata kuliah, angka ringkasan KPI.
* **Body / Konten Standar:** `text-slate-700` (`#334155`) — Label form, isi sel tabel, nama dosen, keterangan deskripsi.
* **Muted / Teks Sekunder:** `text-slate-500` (`#64748B`) — Teks bantuan (*helper text*), placeholder form, metadata waktu.
* **Subtle / Disabling:** `text-slate-400` (`#94A3B8`) — Icon netral, state kontrol yang dinonaktifkan (*disabled*).

### 1.3 Bayangan (*Elevation & Shadows*)
* **Card Container:** `shadow-sm` (`box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05)`) dikombinasikan dengan border `border border-slate-200`.
* **Dropdown & Popover:** `shadow-md` (`box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1)`).
* **Modal Dialog:** `shadow-xl` (`box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1)`).

---

## 2. TIPOGRAFI & ATURAN HIERARKI

### 2.1 Konfigurasi Tipografi
* **Font Family Utama:** `'Plus Jakarta Sans', 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;`
* **Google Fonts Import:**
  ```html
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
  ```

### 2.2 Hierarki Skala Tipografi

| Hierarki | Class Tailwind | Ukuran / Bobot | Penerapan |
| :--- | :--- | :--- | :--- |
| **H1 (Header Utama)** | `text-2xl md:text-3xl font-extrabold text-slate-900 tracking-tight` | 24px - 30px / 800 | Judul dashboard utama aplikasi (*Class Schedule*). |
| **H2 (Section Title)** | `text-lg md:text-xl font-bold text-slate-900` | 18px - 20px / 700 | Judul bagian tabel riwayat, modal form input. |
| **H3 (Card Metric Title)** | `text-sm font-semibold text-slate-500 uppercase tracking-wider` | 14px / 600 | Label atas kartu ringkasan KPI. |
| **KPI Number (Metrik)** | `text-3xl font-bold text-slate-900 tracking-tight` | 30px / 700 | Angka nilai total jadwal, ruangan terpakai, dsb. |
| **Body Regular** | `text-sm font-normal text-slate-700 leading-relaxed` | 14px / 400 | Data teks dalam tabel, isi paragraf deskripsi. |
| **Body Medium / Label** | `text-sm font-medium text-slate-700` | 14px / 500 | Label field formulir (*input label*), header tabel (`th`). |
| **Badge / Caption** | `text-xs font-semibold tracking-wide` | 12px / 600 | Badge hari, badge ruangan, status tag, helper form. |

### 2.3 Format Lokal Indonesia (`id-ID`)
Seluruh representasi waktu, tanggal, dan format numerik wajib menggunakan konvensi format Bahasa Indonesia (`id-ID`):

* **Format Jam / Waktu:**
  * Wajib menggunakan pemisah titik (`.`) atau titik dua standar lokal dengan rentang jelas: `08.00 - 10.00 WIB` atau `08:00 - 10:00`.
* **Format Nama Hari:**
  * Penulisan kapitalisasi baku: `Senin`, `Selasa`, `Rabu`, `Kamis`, `Jumat`, `Sabtu`, `Minggu`.
* **Standard JavaScript Formatter Helper:**
  ```javascript
  // Helper Format Waktu Indonesia
  export const formatJam = (timeStr) => {
    if (!timeStr) return '-';
    // Mengambil HH:MM
    const [hh, mm] = timeStr.split(':');
    return `${hh}.${mm}`;
  };

  // Helper Format Rentang Perkuliahan
  export const formatRentangKuliah = (jamMulai, jamSelesai) => {
    return `${formatJam(jamMulai)} - ${formatJam(jamSelesai)} WIB`;
  };

  // Helper Format Tanggal Indonesia
  export const formatTanggalIndonesia = (dateString) => {
    const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    return new Date(dateString).toLocaleDateString('id-ID', options);
  };
  ```

---

## 3. ATURAN KOMPONEN INTERAKTIF

Seluruh komponen interaktif wajib mematuhi standar desain modern: memiliki *state* jelas (*idle, hover, focus, disabled, loading*), feedback langsung ke pengguna, dan ramah aksesibilitas (*aria-friendly*).

### 3.1 Kartu Ringkasan KPI (*Summary Metric Cards*)
Kartu metrik menggunakan kontainer `bg-white shadow-sm border border-slate-200 rounded-xl p-5`.

```html
<!-- Blueprint Kartu Ringkasan Metrik -->
<div class="bg-white rounded-xl border border-slate-200 shadow-sm p-5 hover:border-slate-300 transition-all duration-200">
  <div class="flex items-center justify-between">
    <div>
      <p class="text-xs font-semibold uppercase tracking-wider text-slate-500">Total Jadwal Aktif</p>
      <h3 class="mt-1 text-3xl font-bold tracking-tight text-slate-900">24</h3>
    </div>
    <div class="flex h-12 w-12 items-center justify-center rounded-xl bg-indigo-50 text-indigo-600">
      <!-- Icon Kalender / Jadwal -->
      <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
      </svg>
    </div>
  </div>
  <div class="mt-4 flex items-center text-xs text-slate-500">
    <span class="inline-flex items-center text-emerald-600 font-semibold mr-1.5">
      <svg class="h-4 w-4 mr-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
      </svg>
      Tersinkronisasi
    </span>
    <span>dengan Supabase PostgreSQL</span>
  </div>
</div>
```

---

### 3.2 Standar Tombol & *Loading State*

#### A. Tombol Primer (Tambah / Simpan Jadwal)
* **Normal State:** `bg-indigo-600 text-white font-semibold px-4 py-2.5 rounded-lg shadow-sm hover:bg-indigo-700 active:bg-indigo-800 transition duration-150 ease-in-out focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2`
* **Loading / Submitting State:**
  * Tambahkan atribut `disabled`.
  * Tambahkan class: `opacity-75 cursor-not-allowed bg-indigo-500`.
  * Ganti teks menjadi *"Menyimpan data..."* atau *"Memeriksa bentrok..."*.
  * Sisipkan animasi SVG spinner berputar (`animate-spin`).

```html
<!-- Blueprint Tombol Saat State Loading -->
<button 
  type="button" 
  disabled 
  class="inline-flex items-center justify-center rounded-lg bg-indigo-500 px-4 py-2.5 text-sm font-semibold text-white shadow-sm opacity-75 cursor-not-allowed transition duration-150">
  <svg class="mr-2 h-4 w-4 animate-spin text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
    <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
    <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8v4a4 4 0 00-4 4H4z"></path>
  </svg>
  Menyimpan Jadwal...
</button>
```

#### B. Tombol Aksi Hapus (*Destructive*)
* `bg-rose-50 text-rose-600 hover:bg-rose-600 hover:text-white border border-rose-200 text-xs font-semibold px-3 py-1.5 rounded-lg transition-colors duration-150`

---

### 3.3 Standar *Empty State* (Saat Tabel Kosong / Tidak Ada Hasil Filter)
Ketika daftar jadwal kosong atau query filter menghasilkan 0 data, sistem **dilarang menampilkan tabel kosong tanpa petunjuk**. Wajib menampilkan komponen *Empty State* yang terstandarisasi:

```html
<!-- Blueprint Empty State Component -->
<div class="flex flex-col items-center justify-center rounded-xl border border-dashed border-slate-300 bg-white p-12 text-center shadow-sm">
  <div class="mx-auto flex h-16 w-16 items-center justify-center rounded-full bg-slate-100 text-slate-400">
    <svg class="h-8 w-8" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5">
      <path stroke-linecap="round" stroke-linejoin="round" d="M19 11H5m14 0a2 2 0 012 2v6a2 2 0 01-2 2H5a2 2 0 01-2-2v-6a2 2 0 012-2m14 0V9a2 2 0 00-2-2M5 11V9a2 2 0 012-2m0 0V5a2 2 0 012-2h6a2 2 0 012 2v2M7 7h10" />
    </svg>
  </div>
  <h3 class="mt-4 text-base font-bold text-slate-900">Belum Ada Jadwal Kuliah</h3>
  <p class="mt-1 max-w-sm text-sm text-slate-500">
    Tidak ada jadwal yang cocok dengan kata kunci pencarian atau filter yang dipilih. Silakan ubah filter atau tambahkan jadwal baru.
  </p>
  <div class="mt-6 flex items-center space-x-3">
    <button type="button" class="inline-flex items-center rounded-lg border border-slate-300 bg-white px-3.5 py-2 text-sm font-semibold text-slate-700 shadow-sm hover:bg-slate-50">
      Reset Filter
    </button>
    <button type="button" class="inline-flex items-center rounded-lg bg-indigo-600 px-4 py-2 text-sm font-semibold text-white shadow-sm hover:bg-indigo-700">
      + Tambah Jadwal Baru
    </button>
  </div>
</div>
```

---

### 3.4 Standar *Alert Banner* Saat Validasi `TC-01` Gagal (Bentrok Terdeteksi)
Sesuai spesifikasi `TC-01` pada SKPL Modul 6, saat terjadi bentrok waktu dan ruangan, sistem wajib menampilkan pesan persis:
> **“Ruang sudah digunakan pada jam tersebut”**

Komponen *Alert Banner* menggunakan palet warna `rose` dengan ikon peringatan (*exclamation triangle*) dan opsi dismiss:

```html
<!-- Blueprint Alert Banner Bentrok Jadwal (TC-01 Failure) -->
<div class="relative rounded-xl border border-rose-200 bg-rose-50 p-4 shadow-sm" role="alert" aria-live="assertive">
  <div class="flex items-start">
    <!-- Icon Warning / Alert -->
    <div class="flex-shrink-0 text-rose-600">
      <svg class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M8.257 3.099c.765-1.36 2.722-1.36 3.486 0l5.58 9.92c.75 1.334-.213 2.98-1.742 2.98H4.42c-1.53 0-2.493-1.646-1.743-2.98l5.58-9.92zM11 13a1 1 0 11-2 0 1 1 0 012 0zm-1-8a1 1 0 00-1 1v3a1 1 0 002 0V6a1 1 0 00-1-1z" clip-rule="evenodd" />
      </svg>
    </div>
    
    <!-- Konten Pesan Bentrok Sesuai SKPL TC-01 -->
    <div class="ml-3 flex-1">
      <h3 class="text-sm font-bold text-rose-900">Validasi Bentrok Jadwal Terdeteksi</h3>
      <div class="mt-1 text-sm text-rose-800">
        <p><strong>Peringatan Sistem:</strong> Ruang sudah digunakan pada jam tersebut.</p>
        <p class="mt-0.5 text-xs text-rose-700">Silakan pilih ruangan lain atau ganti rentang jam perkuliahan agar tidak tumpang tindih.</p>
      </div>
    </div>
    
    <!-- Tombol Tutup Banner -->
    <div class="ml-auto pl-3">
      <div class="-mx-1.5 -my-1.5">
        <button type="button" class="inline-flex rounded-md p-1.5 text-rose-500 hover:bg-rose-100 hover:text-rose-800 focus:outline-none focus:ring-2 focus:ring-rose-500">
          <span class="sr-only">Tutup pemberitahuan</span>
          <svg class="h-4 w-4" viewBox="0 0 20 20" fill="currentColor">
            <path fill-rule="evenodd" d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z" clip-rule="evenodd" />
          </svg>
        </button>
      </div>
    </div>
  </div>
</div>
```

---

### 3.5 Standar Modal Konfirmasi Hapus (*Delete Confirmation Dialog*)
Untuk mencegah penghapusan yang tidak disengaja (*human error*), dialog modal konfirmasi menggunakan backdrop `bg-slate-900/50 backdrop-blur-sm`:

```html
<!-- Blueprint Modal Konfirmasi Hapus -->
<div class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-slate-900/50 backdrop-blur-sm">
  <div class="relative w-full max-w-md rounded-2xl bg-white p-6 shadow-2xl border border-slate-200">
    <div class="flex items-center space-x-3 text-rose-600">
      <div class="flex h-10 w-10 items-center justify-center rounded-full bg-rose-100">
        <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
        </svg>
      </div>
      <h3 class="text-lg font-bold text-slate-900">Konfirmasi Hapus Jadwal</h3>
    </div>
    
    <p class="mt-3 text-sm text-slate-600 leading-relaxed">
      Apakah Anda yakin ingin menghapus data perkuliahan ini? Tindakan ini tidak dapat dibatalkan dan data akan dihapus permanen dari basis data.
    </p>

    <div class="mt-6 flex items-center justify-end space-x-3">
      <button type="button" class="rounded-lg border border-slate-300 bg-white px-4 py-2 text-sm font-semibold text-slate-700 hover:bg-slate-50 transition">
        Batal
      </button>
      <button type="button" class="rounded-lg bg-rose-600 px-4 py-2 text-sm font-semibold text-white shadow-sm hover:bg-rose-700 transition">
        Ya, Hapus Jadwal
      </button>
    </div>
  </div>
</div>
```

---

### 3.6 Standar Form Input & Filter Bar
* **Input Text & Dropdown Select:**
  * Base Class: `w-full rounded-lg border border-slate-300 bg-white px-3.5 py-2 text-sm text-slate-800 placeholder-slate-400 focus:border-indigo-600 focus:outline-none focus:ring-2 focus:ring-indigo-500/20 transition-all`
* **Badge Hari & Ruang di Tabel:**
  * Hari: `inline-flex items-center rounded-full bg-indigo-50 px-2.5 py-0.5 text-xs font-semibold text-indigo-700 border border-indigo-100`
  * Ruang: `inline-flex items-center rounded-full bg-slate-100 px-2.5 py-0.5 text-xs font-semibold text-slate-800 border border-slate-200`
  * Kelas: `inline-flex items-center rounded-md bg-emerald-50 px-2 py-0.5 text-xs font-bold text-emerald-700 border border-emerald-200`

---

## 4. CHECKLIST KEPATUHAN AI / DEVELOPER DI VS CODE

Sebelum menyelesaikan penulisan kode tampilan:
- [x] Latar utama menggunakan `bg-slate-50` dan kontainer kartu menggunakan `bg-white shadow-sm border border-slate-200`.
- [x] Tombol submit memiliki animasi spinner dan teks dinamis saat proses penyimpanan/pengecekan bentrok berlangsung.
- [x] Banner error bentrok menggunakan teks resmi: **“Ruang sudah digunakan pada jam tersebut”** dengan styling `bg-rose-50 border-rose-200 text-rose-800`.
- [x] Penulisan hari menggunakan format Bahasa Indonesia (Senin, Selasa, dst.) dan jam perkuliahan berformat `HH.MM - HH.MM WIB`.
- [x] State tabel kosong (*Empty State*) terpasang dengan instruksi yang ramah pengguna.
- [x] Seluruh input teks disanitasi dari potensi karakter XSS (`SEC-01`).
