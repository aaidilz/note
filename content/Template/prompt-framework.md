---
title: Template Prompt Framework yang Baik (Reusable & Adaptif)
draft: false
tags:
  - prompt-engineering
  - framework
  - ai
  - workflow
---

## Gambaran

Prompt yang baik bukan sekadar “perintah”, tapi struktur yang jelas tentang:

- tujuan
- konteks
- batasan
- output yang diharapkan

Kalau prompt tidak terstruktur, hasilnya sering:

- terlalu umum
- tidak konsisten
- atau melenceng dari kebutuhan

Framework ini dibuat supaya reusable dan bisa dipakai untuk berbagai kasus: coding, security, writing, bahkan game dev.

---

## Struktur Inti Prompt

Gunakan urutan ini:

1. Objective
2. Context
3. Constraints
4. Input (optional)
5. Expected Output
6. Additional Instructions (optional)

---

## Template Dasar

```text
# Objective
Jelaskan tujuan utama secara spesifik.

# Context
Berikan konteks yang relevan:
- lingkungan (tech stack, OS, tools)
- kondisi saat ini
- masalah yang terjadi

# Constraints
Batasan yang harus dipatuhi:
- format output
- larangan tertentu
- gaya penulisan
- scope pekerjaan

# Input
(Data atau contoh yang diberikan ke model)

# Expected Output
Deskripsikan output yang diinginkan secara jelas:
- bentuk (markdown, code, json, dll)
- detail level (ringkas / mendalam)
- struktur

# Additional Instructions
Instruksi tambahan jika ada:
- edge case
- preferensi tertentu
- hal yang harus dihindari
```

---

## Contoh 1 — Prompt Coding

```text
# Objective
Membuat REST API sederhana untuk manajemen user.

# Context
- Backend: Node.js
- Framework: Express
- Database: tidak digunakan (in-memory)

# Constraints
- Tidak menggunakan database
- Gunakan struktur modular
- Hindari library berlebihan

# Expected Output
- Kode lengkap
- Penjelasan singkat tanpa bullet point
```

---

## Contoh 2 — Prompt Cyber Security

```text
# Objective
Menganalisis potensi kerentanan pada endpoint API.

# Context
- Target: Web API
- Fokus: authentication & authorization

# Constraints
- Jangan memberikan eksploitasi langsung
- Fokus pada analisis, bukan attack

# Input
Endpoint: /api/user?id=123

# Expected Output
- Penjelasan potensi vulnerability
- Rekomendasi mitigasi
```

---

## Contoh 3 — Prompt Game Dev

```text
# Objective
Membuat prototype mekanik sniper seperti game Lonewolf.

# Context
- Engine: Unity 2D
- Asset: placeholder
- Fokus pada gameplay, bukan visual

# Constraints
- Gunakan asset sederhana
- Tidak perlu UI kompleks

# Expected Output
- Struktur implementasi
- Script utama
```

---

## Pola Tambahan (Advanced)

Kalau mau lebih presisi, tambahkan layer ini:

### Role Assignment

```text
You are a senior backend engineer with experience in scalable systems.
```

Gunanya untuk mengarahkan gaya berpikir model.

---

### Step-by-Step Reasoning

```text
Jelaskan secara bertahap dari konsep ke implementasi.
```

---

### Output Guard

```text
Jangan menyertakan penjelasan di luar yang diminta.
```

---

### Format Lock

```text
Output harus dalam format markdown tanpa teks tambahan di luar blok.
```

---

## Anti-Pattern (Yang Harus Dihindari)

Prompt seperti ini biasanya bermasalah:

```text
Buatkan aplikasi yang bagus dan keren
```

Masalahnya:

- tidak ada konteks
- tidak ada batasan
- tidak jelas outputnya

Hasilnya pasti random.

---

## Insight

Semakin kompleks task, semakin penting struktur prompt.

Banyak orang mengira model “tidak pintar”, padahal seringnya:
prompt-nya yang ambigu.

Framework ini bukan soal bikin prompt panjang, tapi bikin prompt yang:

- eksplisit
- terarah
- bisa direproduksi

---

## Best Practice

Gunakan iterasi.

Jangan berharap prompt pertama langsung sempurna. Biasanya:

1. Mulai dari template dasar
2. Evaluasi output
3. Tambahkan constraint atau detail
4. Ulangi

Kalau kamu konsisten pakai pola ini, kualitas output akan jauh lebih stabil.
