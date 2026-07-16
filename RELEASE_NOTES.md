# Smart Pro S Firmware 1.0.2 (community build)

Genuine TrimUI **1.0.2** for the Smart Pro S (TG5050), preserved from a retail device — because
TrimUI ships 1.0.2 on hardware but has never released it (their public firmware stops at 1.0.1,
Dec 2025). **Unofficial; not affiliated with TrimUI; use at your own risk.**

## Install — SD card (recommended, no PC)

1. Burn **`sd_recovery_..._v1.0.2_....7z`** → its `.img` to a **spare** microSD, whole-disk
   (balenaEtcher, the bundled Win32DiskImager, or GNOME Disks → *Restore Disk Image*).
2. Device **off** → insert the card → **USB power to the bottom "DC" port** → wait ~10 s for the
   **progress bar**.
3. When it finishes, remove the card and power on. Confirm **Settings → Device Info → 1.0.2**.

**Your games and saves are safe** — they live on your separate game card, which stays *out* of the
device during the flash. Only internal storage (normally empty) is reset.
👉 *Burn to a spare card, not your game card.*

**PC alternative:** flash `trimui_tg5050.awimg` (inside `trimui_..._v1.0.2.7z`) with
PhoenixSuit/LiveSuit, device in Allwinner FEL mode.

## What's new — approximate (reconstructed from a system diff, not official notes)

- **Performance Settings**: power presets + per-CPU-cluster and GPU frequency control
- **Fan control** with temperature-based levels
- **Audio settings**: channel swap, per-channel volume/gain, mic toggle, lower latency
- **SD-card launcher hook** (NextUI/MinUI boot handoff) + boot splash
- Fixes: dual-cluster CPU/temperature overlays, USB-storage game-DB refresh, updated input + Mali
  GPU drivers, updated translations

## Files & checksums (SHA-256)

```
210a8e61edcc463a905fe15ea5f82aae534a754573a326712eeeebd5d79300b8  sd_recovery_tg5050_smart_pro_S_v1.0.2_20260715.7z   (312 MiB) — SD recovery card
b7c26dc730f1d62478cbcb3172e9974d6f3a1d39071518ce57ad8553350461af  trimui_tg5050_20260715_v1.0.2.7z                    (297 MiB) — PhoenixSuit/LiveSuit awimg
```

Revert to official 1.0.1 anytime: <https://github.com/trimui/firmware_smartpro_s>

---
**Unofficial — not affiliated with TrimUI.** Redistributed for interoperability/preservation; we
claim no ownership. Contains open-source (GPL/BSD/MIT/Apache — redistribution permitted) and
proprietary (TrimUI UI, Mali GPU) components. **GPL source:** the corresponding source for the
GPL parts (kernel, U-Boot, BusyBox) is a TrimUI-built Allwinner BSP that TrimUI has not published;
we don't hold it — the obligation is TrimUI's (upstreams: kernel.org, u-boot.org, linux-sunxi.org).
**Rights holders:** open an issue to request source hosting or takedown — handled promptly. As-is,
no warranty. Full terms: `NOTICE.md`.
