# Wisma52 — Project Briefing for Claude Code

## Project overview
Website kosan eksklusif Wisma 52, Jakarta Pusat. Stack: Astro + Tailwind CSS.
Tujuan: website marketing yang clean, minimal, SEO-friendly untuk target profesional muda, karyawan, dokter/koas, dan mahasiswa.

## Tech stack
- Framework: Astro (static site generator)
- Styling: Tailwind CSS + custom CSS variables di global.css
- Fonts: DM Serif Display (headings) + DM Sans (body) via Google Fonts
- Hosting: Vercel
- Domain: https://wisma-52.vercel.app/

## Design system
- Background utama: #fafaf8 (stone-50)
- Text utama: #1a1a18 (stone-950)
- Text muted: #6b6960
- Text tertiary: #9a9890
- Border: #e2e0d8 (0.5px solid — SELALU 0.5px, bukan 1px)
- Font heading: 'DM Serif Display', serif (class `.serif`)
- Font body: 'DM Sans', sans-serif
- Aesthetic: clean minimal, banyak whitespace, tipografi dominan
- NO gradients, NO heavy shadows, NO border-radius besar kecuali WA button
- Layout: full-width sections dengan `.section-full` + `.container` (max-width 1100px, padding 0 48px)
- Full-bleed elements (hero foto, image strip, map, cta-band): `.section-full` tanpa `.container` di dalam
- Mobile: `.container` padding turun ke `0 20px` di bawah 768px
- WaButton: position fixed, z-index 50

## Foto tersedia
- `public/images/eksterior/halaman-parkir.webp`
- `public/images/fasilitas/`: dapur-1.webp, dapur-2.webp, lorong.webp, lorong-2.webp, musholla.webp, musholla-2.webp, ruang-tv.webp, ruang-tv-2.webp, tangga-belakang.webp
- `public/images/kamar/`: kamar-1.webp, kamar-2.webp, kamar-mandi-dalam-1.webp, kamar-mandi-dalam2.webp (tanpa dash sebelum 2)

Path di HTML: `/images/[subfolder]/[nama-file-dengan-ekstensi]`
Gunakan `<img>` biasa (bukan astro:assets) karena file ada di `public/`.
Nama file case-sensitive. Foto baru: copy ke folder yang sesuai, langsung muncul tanpa rebuild.

## Project structure
```
src/
  pages/
    index.astro        ← homepage
    kamar.astro
    fasilitas.astro
    lokasi.astro
    galeri.astro
  components/
    layout/
      BaseLayout.astro  ← wrapper semua halaman (sudah include Navbar, Footer, WaButton)
      Navbar.astro
      Footer.astro
      WaButton.astro
    home/
      Hero.astro
      ImageStrip.astro
      WhyWisma.astro
      RoomPreview.astro
      Reviews.astro
      HomeFaq.astro
    kamar/
      RoomCard.astro
      CompareTable.astro
      PromoBanner.astro
      BookingSteps.astro
    galeri/
      GalleryFilter.astro
      PhotoGrid.astro
    seo/
      SeoHead.astro
      LocalBusinessSchema.astro
    ui/
      Button.astro
      SectionLabel.astro
      CtaBand.astro
  content/
    rooms/
      standard.md
      deluxe.md
      promo.md
    fasilitas/
      kamar.json
      bersama.json
    galeri/
      photos.json
    lokasi/
      nearby.json
  styles/
    global.css
  layouts/
    Base.astro
public/
  images/
    kamar/
    fasilitas/
    eksterior/
  favicon.ico
  og-image.jpg
  robots.txt
```

## Konten bisnis
- Nama: Wisma 52
- Alamat: Jl. Kramat 5 No.2, RT.2/RW.9, Kenari, Senen, Jakarta Pusat 10430
- Samping: Bank BRI Kramat
- WhatsApp admin: 081383667680
- Email: info@wisma52.com
- Jam survei: 08.00–22.00

### Tipe kamar
- Standard: 3×4m, Lantai 1-3, Rp 2.950.000/bulan
- Deluxe: 3×5m, Lantai 1-3, Rp 3.200.000/bulan
- Promo: Lantai 4, Rp 2.300.000/bulan (fasilitas sama dengan Standard)
- Total kamar: 23, khusus single (1 orang), kost campur

### Fasilitas kamar (semua tipe)
AC, kamar mandi dalam, water heater & shower, kloset duduk, TV digital, WiFi included, listrik included, spring bed, lemari, meja kerja, jendela ventilasi

### Fasilitas bersama
Parkir gratis (mobil & motor), CCTV 24 jam, keamanan 24 jam, dapur per lantai, musholla, ruang tamu, akses masuk 24 jam, house-keeping mingguan, kerjasama laundry terdekat

### Lokasi terdekat
- Halte Busway Kramat Raya: 400m, 5 mnt jalan (Koridor 2 & 5)
- Stasiun Cikini: 1.2km, 5 mnt gojek
- Stasiun Senen: 1.5km, 7 mnt gojek
- RSCM: 2km
- RS St. Carolus: 1.8km
- Pertamina Pusat: 1.8km
- UI Salemba: 1.5km

### Peraturan
- 1 orang per kamar (tamu boleh berkunjung)
- Tidak boleh merokok di kamar (boleh di balkon)
- Tidak boleh membawa hewan peliharaan
- Akses 24 jam (tidak ada jam malam)

## SEO notes
- Setiap halaman HARUS punya unique meta title & description
- Halaman lokasi HARUS ada LocalBusiness JSON-LD schema
- Semua halaman HARUS ada canonical URL
- Sitemap otomatis via @astrojs/sitemap

## Coding conventions
- Astro components pakai props yang jelas dengan TypeScript interface
- Styling: Tailwind untuk layout/spacing, custom CSS class untuk design system
- Gambar: pakai `<Image>` dari `astro:assets` untuk optimasi otomatis
- Semua teks konten dalam Bahasa Indonesia
- WhatsApp link format: `https://wa.me/6281383667680?text=...`
- Tidak pakai JavaScript kecuali untuk interaksi yang benar-benar perlu (filter galeri, FAQ accordion)