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
- **SD-card launcher hook** — boot can hand off to `/mnt/SDCARD/.tmp_update/updater`, the hook that
  custom front-ends like **NextUI / MinUI** use, plus a new boot splash.
- **Fixes & updates** — dual-cluster CPU-frequency overlay, corrected temperature reading,
  USB-storage now refreshes the game database after use, updated input + Mali GPU drivers, and
  updated translations.

## Download

Grab the latest [**Release**](../../releases/latest). There are two files — pick one:

| File | Best for | You need |
|---|---|---|
| **`sd_recovery_..._v1.0.2_....7z`** | **most people** — burn to a spare SD card, it auto-flashes | just an SD card |
| `trimui_tg5050_..._v1.0.2.7z` | recovery / PC users | a Windows PC + PhoenixSuit/LiveSuit |

## How to update (SD card — recommended)

### Will I lose my games and saves? **No.**
Your ROMs, games and saves live on your **external microSD game card**, which you take *out* of the
device to make room for the recovery card — so it's never touched. Put it back afterward and
everything is there. The flash only rewrites internal storage, which on this device is normally
empty. **Golden rule: burn the recovery image to a _spare_ card — never your game card.**

### Steps
1. Take a **spare** microSD (its contents get erased); a plain **≤ 32 GB** card is safest.
2. Extract the `sd_recovery_...7z` and write the `.img` **to the whole card** with
   [balenaEtcher](https://etcher.balena.io/), the bundled `Win32DiskImager`, or GNOME Disks →
   *Restore Disk Image* (pick the **drive**, not a partition). Don't copy the `.img` in as a file.
3. Turn the device **off** (hold Power ~20 s if you're unsure).
4. Insert the card, plug **USB power into the bottom "DC" port** (a charger works — *not* the top
   port), and press nothing. After ~10 s a **progress bar** appears and flashes the firmware.
5. When it finishes, **remove the card and power on** (a manual reboot at the end is normal).
6. Check **Settings → Device Info** — it should read **1.0.2**. Put your game card back. Done.

Prefer a PC? Flash `trimui_tg5050.awimg` (from the other archive) with PhoenixSuit/LiveSuit, device
in Allwinner FEL mode, DC port to the PC.

## If something goes wrong

You can always return to official **1.0.1** with TrimUI's own release:
[`trimui/firmware_smartpro_s`](https://github.com/trimui/firmware_smartpro_s) — flash its
`sd_recovery` card exactly the same way. The SD recovery flow is designed to rescue a bricked unit,
so this is low-risk — but **you do it at your own risk.**

## Checksums (SHA-256)

Verify your download before flashing:

```
210a8e61edcc463a905fe15ea5f82aae534a754573a326712eeeebd5d79300b8  sd_recovery_tg5050_smart_pro_S_v1.0.2_20260715.7z
b7c26dc730f1d62478cbcb3172e9974d6f3a1d39071518ce57ad8553350461af  trimui_tg5050_20260715_v1.0.2.7z
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
