---
title: Ubuntu 26.04 Fresh Install Setup Guide
draft: false
tags: [ubuntu, setup, optimization, cli, linux]
---

## Update & Upgrade Repository

Langkah pertama setelah fresh install adalah memastikan semua package up-to-date:

```bash
sudo apt update && sudo apt upgrade -y
```

---

## Install Timeshift + Auto Backup

Install Timeshift untuk sistem snapshot:

```bash
sudo apt install timeshift -y
```

Jalankan konfigurasi awal:

```bash
sudo timeshift-gtk
```

Pilih:

- Mode: RSYNC
- Schedule: Weekly
- Keep: 2 snapshots

---

## Install Aplikasi Utama

### MPV (APT)

```bash
sudo apt install mpv -y
```

### Brave (Snap)

```bash
sudo snap install brave
```

### OnlyOffice (Snap)

```bash
sudo snap install onlyoffice-desktopeditors
```

---

## Install NVM + Gemini CLI

Install NVM (Node Version Manager):

````bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.4/install.sh | bash```

Load NVM in the current shell:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
````

Add the following to `~/.bashrc`, `~/.zshrc`, or the shell config you use:

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"
```

Install the latest LTS version of Node.js and set it as default:

```bash
nvm install --lts
nvm alias default 'lts/*'
```

Verify Node.js and npm:

```bash
node -v
npm -v
```

Install Gemini CLI globally:

```bash
npm install -g @google/gemini-cli
```

---

## Install Visual Studio Code (Snap)

```bash
sudo snap install code --classic
```

---

## Optimasi Boot Time

Kurangi delay saat boot:

```bash
sudo systemctl disable NetworkManager-wait-online.service
```

---

## (Optional) Setup ZRAM + Swap Optimization (Low RAM)

Install ZRAM:

```bash
sudo apt install zram-tools -y
```

---

### Set Swap ke 8GB

```bash
sudo swapoff -a
sudo fallocate -l 8G /swap.img
sudo chmod 600 /swap.img
sudo mkswap /swap.img
sudo swapon /swap.img
```

Tambahkan ke fstab:

```bash
echo '/swap.img none swap sw 0 0' | sudo tee -a /etc/fstab
```

---

Dengan konfigurasi ini:

- ZRAM aktif (compressed RAM)
- Swap disk = 8GB
- Total virtual memory ≈ 12GB (tergantung RAM)
