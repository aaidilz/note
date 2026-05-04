---
Title: Assembly untuk Reverse Engineering (Fokus Praktis & Mendalam)
draft: false
tag:
  - reverse-engineering
  - assembly
  - low-level
---

# Assembly untuk Reverse Engineering

Kalau dibawa ke konteks reverse engineering, assembly bukan lagi “bahasa pemrograman”, tapi **alat baca pikiran program**. Kamu tidak menulis dari nol, tapi membaca hasil transformasi compiler yang sering sudah “tidak ramah manusia”.

Masalah utamanya:

- Tidak ada nama variabel
- Tidak ada komentar
- Struktur high-level hilang

Jadi yang kamu lakukan adalah:

> mengubah instruksi mesin → menjadi logika yang bisa dimengerti

---

# 1. Arsitektur: x86 vs x64 (Fokus Praktis)

Kebanyakan target modern:

- Windows → x64 (PE)
- Linux → x64 (ELF)

Perbedaan penting:

| x86             | x64                |
| --------------- | ------------------ |
| eax, ebx        | rax, rbx           |
| 32-bit          | 64-bit             |
| stack-based arg | register-based arg |

---

## Calling Convention (WAJIB PAHAM)

Di x64 (System V / Linux):

| Arg | Register |
| --- | -------- |
| 1   | rdi      |
| 2   | rsi      |
| 3   | rdx      |
| 4   | rcx      |
| 5   | r8       |
| 6   | r9       |

Return value:

- `rax`

---

### Insight penting:

Kalau kamu lihat:

```asm
mov rdi, input
mov rsi, password
call strcmp
```

Langsung tahu:

> fungsi menerima 2 parameter → kemungkinan string compare

---

# 2. Register yang Sering Muncul

## General Purpose

- `rax` → return value
- `rbx` → general
- `rcx` → counter / arg
- `rdx` → arg / data
- `rsi` → source
- `rdi` → destination

---

## Stack Pointer & Frame

- `rsp` → stack pointer
- `rbp` → base pointer

---

## Contoh Stack Frame

```asm
push rbp
mov rbp, rsp
sub rsp, 0x20
```

Artinya:

- bikin ruang stack untuk variabel lokal

---

# 3. Akses Variabel (Ini yang sering bikin bingung)

Contoh:

```asm
mov eax, [rbp-4]
```

Artinya:

- ambil variabel lokal

```asm
mov eax, [rbp+8]
```

Artinya:

- parameter fungsi

---

## Insight:

| Offset  | Arti              |
| ------- | ----------------- |
| rbp - X | local variable    |
| rbp + X | argument / return |

---

# 4. Control Flow (Kunci Reverse)

## Perbandingan

```asm
cmp eax, 5
je label_true
```

Artinya:

- kalau eax == 5 → lompat

---

## Mapping ke High-Level

| Assembly | High-Level |
| -------- | ---------- |
| je       | ==         |
| jne      | !=         |
| jl       | <          |
| jg       | >          |

---

## Contoh Real

```asm
cmp eax, 0
jne fail
```

Interpretasi:

```c
if (eax != 0) {
    fail();
}
```

---

# 5. Loop

## Contoh Assembly

```asm
mov ecx, 5
loop_start:
dec ecx
jnz loop_start
```

Artinya:

- loop 5 kali

---

## Mapping

```c
for (int i = 5; i > 0; i--)
```

---

# 6. Function Call

```asm
call function
```

Setelah call:

- return value di `rax`

---

## Contoh:

```asm
call strlen
cmp rax, 8
```

Artinya:

```c
if (strlen(input) == 8)
```

---

# 7. Pola Penting dalam Reverse

Ini bagian yang bikin kamu naik level.

---

## 1. String Comparison

```asm
call strcmp
test eax, eax
je success
```

Pattern:

- `eax == 0` → sama

---

## 2. Password Check Manual

```asm
mov al, [rdi]
cmp al, 'A'
jne fail
```

Artinya:

- karakter pertama harus 'A'

Biasanya ini diulang → berarti password dicek per karakter

---

## 3. XOR Obfuscation

```asm
xor eax, eax
```

= set ke 0

---

```asm
xor byte ptr [rbp-1], 0x41
```

= decode sederhana

---

## Insight:

XOR sering dipakai untuk:

- obfuscation
- encoding ringan

---

# 8. Memory & Pointer

## Pointer dereference

```asm
mov eax, [rax]
```

Artinya:

- ambil isi dari alamat rax

---

## Double pointer

```asm
mov rax, [rbp-8]
mov eax, [rax]
```

Artinya:

- pointer ke pointer

---

# 9. Stack Behavior

## Push & Pop

```asm
push rax
pop rbx
```

Artinya:

- simpan → ambil kembali

---

## Return

```asm
ret
```

= kembali ke caller

---

# 10. Contoh Reverse (Langkah Nyata)

## Assembly Target

```asm
mov rdi, input
call strlen
cmp rax, 5
jne fail

mov al, [input]
cmp al, 'H'
jne fail

mov al, [input+1]
cmp al, 'E'
jne fail

jmp success
```

---

## Cara Berpikir

Jangan baca baris per baris dulu.

Cari pola:

1. Ada `strlen`
2. Ada compare per karakter

---

## Interpretasi

```c
if (strlen(input) != 5) fail;

if (input[0] != 'H') fail;
if (input[1] != 'E') fail;

success();
```

---

## Insight:

Reverse bukan baca kode,
tapi:

> mengenali pola logika

---

# 11. Kesalahan Umum

## 1. Terlalu Literal

Baca assembly satu per satu → salah

Harus:

- lihat pattern
- lihat tujuan

---

## 2. Tidak Tracking Register

Kalau kamu tidak tahu isi register:

- kamu buta alur program

---

## 3. Mengabaikan Calling Convention

Ini bikin:

- salah interpretasi parameter

---

# 12. Strategi Efektif (Yang Dipakai Praktisi)

## 1. Tandai Entry Point

Biasanya:

- main
- fungsi validasi

---

## 2. Cari Decision Node

- cmp
- test
- jump

---

## 3. Reconstruct Logic

Dari:

- jump → if
- loop → for

---

## 4. Verifikasi dengan Debugger

Static → hipotesis
Dynamic → bukti

---

# 13. Mindset Penting

Assembly itu tidak “rumit”,
yang rumit itu:

- jumlah detailnya
- cara kita melihatnya

Kalau kamu sudah terbiasa:

```asm
cmp eax, 0
je success
```

langsung kebaca:

> "ini validasi"

---

# Penutup

Assembly dalam reverse engineering bukan soal hafal instruksi, tapi:

- mengenali pola
- memahami alur data
- memahami alur kontrol

Kalau diringkas:

> Register = variabel
> Memory = storage
> Jump = logika
> Call = fungsi

Dan tugas kamu:

> mengubah semua itu kembali menjadi “cerita program”
