---
Title: Fix Unity Missing libxml2.so.2 on Ubuntu 26.04
draft: false
tag:
  - unity
  - linux
  - troubleshooting
---

# Solving Missing libxml2.so.2 for Unity on Ubuntu 26.04

## Issue

When running the Unity Editor, the following error occurred:
`./Unity: error while loading shared libraries: libxml2.so.2: cannot open shared object file: No such file or directory`

## Root Cause

Unity 2022.3 expects `libxml2.so.2`. However, Ubuntu 26.04 (Resolute Raccoon) ships with a newer version of the library, `libxml2.so.16`.

## Solution

Since `libxml2.so.16` is largely backward compatible for the functions required by Unity, the issue was resolved by creating a symbolic link in the Unity Editor directory. This allows the Unity executable to find the library via its `RUNPATH`.

### Steps Taken:

1. Identified the location of the system's `libxml2.so.16`:
   `/usr/lib/x86_64-linux-gnu/libxml2.so.16`
2. Created a symlink named `libxml2.so.2` in the Unity Editor directory pointing to the system library:
   ```bash
   ln -s /usr/lib/x86_64-linux-gnu/libxml2.so.16 /home/oguri/Unity/Hub/Editor/2022.3.62f3/Editor/libxml2.so.2
   ```

## Verification

The fix was verified by running Unity in batch mode:

```bash
./Unity -batchmode -quit -logFile -
```

The editor initialized successfully and exited without library errors.
