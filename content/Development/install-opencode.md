---
title: OpenCode Setup Guide
draft: false
tags: [opencode, setup, cli, mcp, plugin]
---

## Install OpenCode

Gunakan perintah berikut untuk menginstall OpenCode melalui terminal:

```bash
curl -fsSL https://opencode.ai/install.sh | sh
```

## Konfigurasi Skill

Setelah instalasi selesai, jalankan konfigurasi skill menggunakan:

```bash
npx skill
```

Ikuti instruksi interaktif untuk menambahkan atau mengatur skill sesuai kebutuhan.

## Konfigurasi MCP

Tambahkan MCP (Model Context Protocol) menggunakan perintah:

```bash
opencode mcp add
```

Sesuaikan dengan endpoint atau konfigurasi MCP yang ingin digunakan.

## Menambahkan Plugin

Untuk memperluas fitur OpenCode, kamu bisa menambahkan plugin seperti:

### opencode-mem

```bash
opencode plugin add opencode-mem
```

### oh-my-opencode

```bash
opencode plugin add oh-my-opencode
```

Setelah plugin terpasang, lakukan restart jika diperlukan agar konfigurasi aktif sepenuhnya.
