# TrimUI Smart Pro S — Firmware 1.0.2 (community build)

**Unofficial, community-preserved firmware for the TrimUI Smart Pro S (model TG5050).**
Not affiliated with or endorsed by TrimUI. Use at your own risk.

## Why this exists

New Smart Pro S units have been shipping with firmware **1.0.2** preinstalled (build dated early
2026) — but TrimUI has **never published 1.0.2** as a downloadable release. As of mid-2026 their
official firmware still stops at **1.0.1** (18 Dec 2025). That leaves owners stuck:

- If you're still on 1.0.1, there's no official way to move up to 1.0.2.
- If you ever reflash, downgrade, or recover your device, you can't get 1.0.2 back.

So we dumped a genuine 1.0.2 image from a retail Smart Pro S and repacked it into TrimUI's **own
flashable formats** — the exact kinds of files an official release ships — so any Smart Pro S owner
can install or restore 1.0.2.

**This is TrimUI's real 1.0.2**: the kernel and system are byte-for-byte what shipped on the device.
The only change is that per-device secrets from the donor unit (its saved Wi-Fi password and SSH
host keys) were removed for privacy. See [How it was built](#how-it-was-built).

## What's new in 1.0.2

> ⚠️ **Approximate.** Reconstructed by diffing the 1.0.1 vs 1.0.2 system, *not* from official
> release notes. Feature names are taken from the firmware's own on-screen text.

- **Performance Settings** — power-mode presets (Power Saving / Balanced / Performance), per-CPU-
  cluster min/max frequency, and GPU max frequency.
- **Fan control** — a Fan setting with an on-screen level stepper; the fan now ramps with
  temperature and stops on sleep.
- **Audio settings** — speaker/headphone channel swap, per-channel volume, gain, mic toggle, and
  lower audio latency.
- **Fixes & updates** — dual-cluster CPU-frequency overlay, corrected temperature reading,
  USB-storage now refreshes the game database after use, updated input + Mali GPU drivers, and
  updated translations.

## Download

Grab the latest [**Release**](../../releases/latest). There are two files — pick one:

| File | Best for | You need |
|---|---|---|
| **`trimui_tg5050_..._v1.0.2.7z`** | **most people** — copy one file to any FAT32 SD card, no disk imager | any microSD card |
| `sd_recovery_..._v1.0.2_....7z` | rescue / won't-boot situations — whole-disk image, provides its own boot chain | spare SD card + disk imager |

## Will I lose my games and saves? **No.**

The flash only rewrites the OS partitions (kernel, system, bootloader). It does **not** touch:

- Your **external microSD game card** — it's never accessed during flashing.
- Your **internal game/save storage** (the UDISK area of the eMMC) — it sits outside the
  partitions that get flashed and is left completely intact.

In short: your games and saves are safe regardless of where you keep them.

## How to update

### Option A — file copy, no disk imager (recommended)

1. Format a microSD card as **FAT32** (any size ≥ 1 GB works; you can use your game card if it's
   FAT32 and has room, or a spare card).
2. Extract `trimui_tg5050.awimg` from `trimui_tg5050_..._v1.0.2.7z` and copy it to the **root**
   of the card. No other files needed.
3. Turn the device **off** (hold Power ~20 s if you're unsure).
4. Insert the card, hold **Vol−**, and press **Power**. After ~10 s a **progress bar** appears and
   flashes the firmware.
5. When it finishes, **remove the card and power on**.
6. Check **Settings → Device Info** — it should read **1.0.2**. Done.

### Option B — whole-disk SD recovery image (fallback / rescue)

Use this if Option A doesn't work, or if the device is in a state where it won't boot at all. It
provides its own boot chain and can recover a bricked unit.

1. Take a **spare** microSD (≤ 32 GB recommended; its entire contents get erased).
2. Extract `sd_recovery_..._v1.0.2_....7z` and write the `.img` **to the whole card** with
   [balenaEtcher](https://etcher.balena.io/), the bundled `Win32DiskImager`, or GNOME Disks →
   *Restore Disk Image* (pick the **drive**, not a partition). Don't copy the `.img` as a file.
3. Turn the device **off**.
4. Insert the card, plug **USB power into the bottom "DC" port** (not the top port), and press
   nothing. After ~10 s a **progress bar** appears and flashes the firmware.
5. When it finishes, **remove the card and power on**.
6. Check **Settings → Device Info** — it should read **1.0.2**. Done.

### Option C — PC (PhoenixSuit / LiveSuit)

Flash `trimui_tg5050.awimg` (from the same archive as Option A) with PhoenixSuit or LiveSuit,
device in Allwinner FEL mode (hold Vol− while plugging USB to PC), DC port to the PC.

## If something goes wrong

You can always return to official **1.0.1** with TrimUI's own release:
[`trimui/firmware_smartpro_s`](https://github.com/trimui/firmware_smartpro_s) — flash its
`sd_recovery` card using Option B above. The SD recovery flow is designed to rescue a bricked unit,
so this is low-risk — but **you do it at your own risk.**

## Checksums (SHA-256)

Verify your download before flashing:

```
24b7d4d488ba4d1c7cd15485f552e6142e1cef864c470f544194c1fa132360e3  sd_recovery_tg5050_smart_pro_S_v1.0.2_20260715.7z
e57ae26557df31bfe14a9f0f45917fc3f2fcb18f814a30ac17e8a283857e8a82  trimui_tg5050_20260715_v1.0.2.7z
```

## How it was built

We dumped the eMMC of a retail 1.0.2 unit, then repacked **only the two partitions that differ from
1.0.1** (`boot` and `rootfs`) into TrimUI's IMAGEWTY / PhoenixCard formats — every bootloader and
config file is byte-identical to the official 1.0.1 release. The donor unit's Wi-Fi credentials and
SSH host keys were stripped and the free space zeroed, so no personal data remains. See
[`NOTICE.md`](NOTICE.md) for licensing and open-source / source-code details.

## Licensing, attribution & takedown

**Unofficial community project — not affiliated with, authorized by, or endorsed by TrimUI.**
"TrimUI" and product names are trademarks of their respective owners, used here only to identify
the hardware this firmware runs on. This repo redistributes TrimUI's stock firmware for
**interoperability and preservation**; we claim no ownership of it and add no license of our own.

The image mixes **free/open-source software** (Linux kernel, U-Boot, BusyBox and other
GPL/BSD/MIT/Apache components — redistribution permitted) with **proprietary components** (TrimUI's
UI software and the ARM Mali GPU driver, which remain their owners' copyright).

**GPL source:** this image contains GPLv2 software (kernel, U-Boot, BusyBox). The GPL requires
corresponding source to be available. **We don't have it** — it's a modified Allwinner BSP built by
TrimUI, who hasn't published the source; that obligation rests with TrimUI. Upstreams:
[kernel.org](https://kernel.org), [u-boot.org](https://u-boot.org),
[linux-sunxi.org](https://linux-sunxi.org). If corresponding source is published we'll link/mirror
it on request.

**Takedown:** if you're TrimUI or a rights holder and want this removed, **open an issue** — it will
be taken down promptly. Provided **as-is, no warranty**; you assume all risk.

Full statement: [`NOTICE.md`](NOTICE.md).
