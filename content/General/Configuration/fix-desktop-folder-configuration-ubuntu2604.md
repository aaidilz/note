---
Title: Fix Desktop Folder Configuration on Ubuntu 26.04
draft: false
tag:
  - linux
  - desktop
  - troubleshooting
---

# Desktop Configuration Solver

## Problem

The desktop was displaying all files and folders located in the home directory (`~/`). This occurred because the XDG Desktop path was incorrectly set to the root of the home folder.

## Diagnosis

- Checked `~/.config/user-dirs.dirs`, which showed:
  ```bash
  XDG_DESKTOP_DIR="$HOME/"
  XDG_DOWNLOAD_DIR="$HOME/"
  ...
  ```
- Confirmed with `xdg-user-dir DESKTOP` returning `/home/oguri/`.

## Solution

Reset the XDG user directories to their standard subfolder locations.

### Steps Taken:

1.  **Created standard directories**:
    ```bash
    mkdir -p ~/Desktop ~/Downloads ~/Templates ~/Public ~/Music ~/Videos
    ```
2.  **Updated `~/.config/user-dirs.dirs`**:
    Changed the paths from `$HOME/` to their respective subfolders (e.g., `XDG_DESKTOP_DIR="$HOME/Desktop"`).
3.  **Applied changes**:
    ```bash
    xdg-user-dirs-update
    ```

## Verification

- Running `xdg-user-dir DESKTOP` now correctly returns `/home/oguri/Desktop`.
- (Note: A session restart or file manager restart may be required for the GUI to update visually.)
