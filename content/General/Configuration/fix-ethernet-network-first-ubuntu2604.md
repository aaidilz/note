---
Title: Fix Ethernet Network First on Ubuntu 26.04
draft: false
tag:
  - linux
  - network
  - troubleshooting
---

# Network Troubleshooting Solver

## Problem

The ethernet connection was active but there was no internet access. The interface was assigned a link-local IP address (169.254.x.x), indicating it wasn't receiving a configuration from the DHCP server.

## Diagnosis

1.  **Interface Status**: Checked using `ip addr`, which showed `enp0s31f6` with `169.254.109.246/16`.
2.  **Connection Profile**: Checked using `nmcli connection show netplan-enp0s31f6`, which revealed `ipv4.method: link-local`.
3.  **Netplan Configuration**: Examined `/etc/netplan/00-installer-config.yaml`, which was missing the `dhcp4: true` directive.

## Solution

Modified the Netplan configuration to enable DHCP4 for the ethernet interface.

### Steps Taken:

1.  Updated `/etc/netplan/00-installer-config.yaml`:
    ```yaml
    network:
      version: 2
      ethernets:
        enp0s31f6:
          match:
            macaddress: "e8:6a:64:59:34:98"
          set-name: "enp0s31f6"
          dhcp4: true
    ```
2.  Applied the changes:
    ```bash
    sudo netplan apply
    ```

## Verification

- `ip addr show enp0s31f6` now shows a valid dynamic IP address (`172.16.13.227`).
- `ping -c 4 google.com` confirms active internet connectivity.
