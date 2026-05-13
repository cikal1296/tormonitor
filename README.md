<div align="center">

# Monitor Detection AI

**Deteksi status monitor nyala / mati secara real-time.**  
Model YOLO11n berjalan langsung di browser — tanpa server, tanpa kirim data ke mana pun.

[![Live Demo](https://img.shields.io/badge/Live%20Demo-Visit%20Site-00e87a?style=for-the-badge)](https://detect-monitor.vercel.app)
[![Model](https://img.shields.io/badge/Model-YOLO11n%20ONNX-5c6fff?style=for-the-badge)](#model-info)
[![License](https://img.shields.io/badge/License-AGPL--3.0-ff4455?style=for-the-badge)](https://www.gnu.org/licenses/agpl-3.0)

</div>

---

## Cara Pakai

Buka situsnya, lalu pilih salah satu:

- **Kamera** — klik *Buka Kamera*, izinkan akses, deteksi berjalan otomatis real-time
- **Upload gambar** — klik *Upload Gambar* atau drag & drop file ke area viewport
- **Paste** — tekan `Ctrl+V` untuk paste gambar langsung dari clipboard
- **Snapshot** — saat kamera aktif, klik *Snapshot* untuk simpan frame dengan bounding box

Tidak perlu install apapun. Tidak perlu akun. Buka dan langsung jalan.

---

## Fitur

| | |
|---|---|
| 🔒 **100% Privat** | Semua inferensi di browser. Gambar tidak pernah meninggalkan perangkat. |
| ⚡ **Real-time** | Deteksi dari stream kamera tiap ~120ms menggunakan WebGL atau WASM. |
| 🎯 **3 Kelas** | Mendeteksi monitor `menyala`, `mati`, dan `objects` lain. |
| 📸 **Snapshot** | Simpan frame kamera lengkap dengan bounding box hasil deteksi. |
| 🖱️ **Drag & Drop** | Drop gambar langsung ke halaman, atau paste dari clipboard. |
| 📱 **Responsive** | Bisa dipakai di desktop maupun HP. |

---

## Model Info

| Property | Value |
|----------|-------|
| Architecture | YOLO11n |
| Format | ONNX (IR v9, Opset 20) |
| Input shape | `[1, 3, 640, 640]` |
| Output shape | `[1, 7, 8400]` |
| Classes | `mati`, `menyala`, `objects` |
| Confidence threshold | 0.25 |
| NMS IoU threshold | 0.45 |
| File size | ~11 MB |
| Backend | WebGL (GPU) → fallback WASM |

---

## Struktur Repo

```
detect-monitor/
├── index.html        # Seluruh app — UI, logic inferensi, CSS dalam satu file
├── vercel.json       # CORS headers (COOP + COEP) untuk WASM threads
└── model/
    └── best.onnx     # Model YOLO11n (~11MB)
```

---

## Deploy Sendiri

### GitHub Pages

1. Fork repo ini
2. Masuk ke **Settings → Pages**
3. Source: `Deploy from a branch` → branch `main` → folder `/root`
4. Klik **Save**

> ⚠️ GitHub Pages tidak support custom headers, jadi WASM multi-threading dinonaktifkan otomatis. WebGL tetap jalan normal.

### Vercel (Recommended)

1. Import repo ke [vercel.com](https://vercel.com)
2. Set konfigurasi berikut:

   | Setting | Value |
   |---|---|
   | Framework Preset | `Other` |
   | Build Command | *(kosongkan)* |
   | Output Directory | *(kosongkan)* |

3. Klik **Deploy** — `vercel.json` sudah otomatis mengatur COOP/COEP headers.

---

## Teknologi

- [ONNX Runtime Web](https://onnxruntime.ai) — inferensi model di browser via WebGL / WASM
- [YOLO11n](https://docs.ultralytics.com) — arsitektur deteksi objek ringan dari Ultralytics
- Vanilla JS + HTML Canvas — tanpa framework, tanpa build step

---

## Lisensi

Model (`best.onnx`) dilisensikan di bawah **AGPL-3.0** mengikuti lisensi Ultralytics.  
Kode UI/app bebas dipakai dan dimodifikasi.
