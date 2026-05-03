---
title: Konfigurasi Networking Waydroid + Firewall (Ubuntu)
draft: false
tags:
  - waydroid
  - networking
  - firewall
  - android
  - linux
---

## Gambaran Masalah

Secara default, Waydroid berjalan menggunakan network bridge (biasanya `waydroid0`) yang dibuat oleh container system (LXC). Android di dalam Waydroid tidak langsung “terlihat” ke jaringan luar karena:

- NAT digunakan
- Firewall Linux bisa memblokir trafik
- IP Waydroid berbeda dari host

Kalau networking tidak dikonfigurasi dengan benar, biasanya gejalanya:

- Tidak bisa akses internet dari Waydroid
- Tidak bisa diakses dari device lain
- ADB over network tidak jalan

---

## Cek Interface Waydroid

Pertama, pastikan interface muncul:

```bash
ip a | grep waydroid
```

Biasanya muncul seperti:

```text
waydroid0
```

Kalau tidak ada, berarti service belum jalan:

```bash
sudo systemctl start waydroid-container
```

---

## Enable IP Forwarding

Agar trafik bisa lewat dari Waydroid ke luar:

```bash
sudo sysctl -w net.ipv4.ip_forward=1
```

Supaya permanen:

```bash
sudo nano /etc/sysctl.conf
```

Tambahkan:

```conf
net.ipv4.ip_forward=1
```

Apply:

```bash
sudo sysctl -p
```

---

## NAT dengan iptables

Ini bagian penting supaya Waydroid bisa akses internet.

Misal interface internet `wlan0` atau `eth0`:

```bash
sudo iptables -t nat -A POSTROUTING -o wlan0 -j MASQUERADE
```

Izinkan forwarding:

```bash
sudo iptables -A FORWARD -i waydroid0 -o wlan0 -j ACCEPT
sudo iptables -A FORWARD -i wlan0 -o waydroid0 -m state --state RELATED,ESTABLISHED -j ACCEPT
```
