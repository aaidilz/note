---
title: Install Flutter on Ubuntu Without Android Studio
draft: false
tags:
  - flutter
  - ubuntu
  - development
  - mobile
  - setup
---

## Gambaran

Setup ini fokus ke environment CLI tanpa Android Studio. Cocok kalau kamu ingin setup ringan, reproducible, atau dipakai di server/dev environment minimal.

Alur yang dipakai:

1. Install Flutter via snap
2. Install Android Command Line Tools manual
3. Install SDK components via sdkmanager
4. Set environment variables
5. Verifikasi dengan flutter doctor

---

## 1. Install Flutter SDK (Snap)

```bash
sudo snap install flutter --classic
```

Cek:

```bash
flutter --version
```

Kalau command tidak dikenali, kemungkinan PATH belum terbaca. Biasanya snap sudah auto handle, tapi kadang perlu relogin shell.

---

## 2. Install Android Command Line Tools

Download dari:

[https://developer.android.com/studio#command-line-tools-only](https://developer.android.com/studio#command-line-tools-only)

Ambil yang **command line tools only (Linux)**.

---

### Extract ke direktori SDK

Misalnya:

```bash
mkdir -p $HOME/Android/Sdk/cmdline-tools
cd $HOME/Android/Sdk/cmdline-tools
```

Extract:

```bash
unzip ~/Downloads/commandlinetools-linux-*.zip
```

Rename agar sesuai struktur yang diharapkan:

```bash
mv cmdline-tools latest
```

Struktur akhir harus seperti ini:

```text
$HOME/Android/Sdk/cmdline-tools/latest/bin/sdkmanager
```

Kalau tidak sesuai, error klasik yang muncul:

- `cmdline-tools component is missing`
- `Could not determine SDK root`

---

## 3. Install SDK Components (sdkmanager)

Masuk ke folder:

```bash
cd $HOME/Android/Sdk/cmdline-tools/latest/bin
```

Install komponen penting:

```bash
./sdkmanager --sdk_root=$HOME/Android/Sdk \
"platform-tools" \
"platforms;android-34" \
"build-tools;34.0.0" \
"cmdline-tools;latest"
```

Terima license:

```bash
./sdkmanager --licenses
```

---

## 4. Set Environment Variables (.bashrc)

Edit:

```bash
nano ~/.bashrc
```

Tambahkan:

```bash
export ANDROID_HOME=$HOME/Android/Sdk
export ANDROID_SDK_ROOT=$ANDROID_HOME

export PATH=$PATH:$ANDROID_HOME/platform-tools
export PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest/bin
export PATH=$PATH:$ANDROID_HOME/emulator
```

Apply:

```bash
source ~/.bashrc
```

---

## 5. Integrasi Flutter dengan Android SDK

Set path SDK:

```bash
flutter config --android-sdk $HOME/Android/Sdk
```

---

## 6. Verifikasi

```bash
flutter doctor
```

Kalau masih error:

### Kasus umum

#### 1. cmdline-tools not found

Biasanya struktur folder salah (tidak ada `latest/`)

#### 2. licenses belum accepted

Jalankan ulang:

```bash
sdkmanager --licenses
```
