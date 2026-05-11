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

# Waydroid Network Fix Guide

This document outlines the steps to resolve network connectivity issues in Waydroid by creating a NetworkManager-managed bridge.

## Problem Description

Waydroid often fails to establish a network connection because the `waydroid0` interface is either DOWN or lacks proper NAT/IP masquerading rules on the host. This results in the Android container having no internet access despite the host being connected.

## Solution: NetworkManager Bridge

The most robust solution on systems using NetworkManager is to delegate the management of the `waydroid0` interface to NetworkManager. This automatically handles DHCP, DNS, and NAT (via the `shared` IPv4 method).

### Steps to Apply Fix

1.  **Stop Waydroid (optional but recommended):**

    ```bash
    sudo waydroid container stop
    ```

2.  **Create the bridge connection:**

    ```bash
    sudo nmcli con add type bridge ifname waydroid0 con-name waydroid0 autoconnect yes
    ```

3.  **Configure IPv4 sharing:**
    This step enables NAT and sets the host as a gateway.

    ```bash
    sudo nmcli con modify waydroid0 ipv4.method shared
    ```

4.  **Ignore IPv6 (prevents potential conflicts):**

    ```bash
    sudo nmcli con modify waydroid0 ipv6.method ignore
    ```

5.  **Bring the connection up:**

    ```bash
    sudo nmcli con up waydroid0
    ```

6.  **Restart Waydroid Container:**
    ```bash
    sudo systemctl restart waydroid-container
    ```

## Verification

### 1. Check Host Interface

Ensure `waydroid0` has an IP address (usually `10.42.0.1`):

```bash
ip addr show waydroid0
```

### 2. Check Container Connectivity

Ensure the Waydroid session is running (`waydroid session start` or similar) before testing:

```bash
# Test IP connectivity
echo "ping -c 3 8.8.8.8" | sudo waydroid shell

# Test DNS resolution
echo "ping -c 3 google.com" | sudo waydroid shell
```

## Troubleshooting

- **Interface state DOWN:** If `waydroid0` shows `state DOWN` or `NO-CARRIER`, ensure the Waydroid container is actually running and has attempted to use the network.
- **Shared method fails:** Ensure NetworkManager has the `dnsmasq` or equivalent internal DHCP provider active (this is usually default).
- **Firewall:** Double check `ufw status`. If active, ensure the routes are allowed.
