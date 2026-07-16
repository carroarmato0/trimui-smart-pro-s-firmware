# Notice — licensing, attribution & legal

This project redistributes a copy of **TrimUI's stock firmware** for the TrimUI Smart Pro S
(model TG5050), for **interoperability and preservation** — so owners can install version 1.0.2,
which TrimUI ships preinstalled on hardware but has not published for download.

## Not affiliated with TrimUI

This is an **unofficial community project. It is not affiliated with, authorized by, sponsored by,
or endorsed by TrimUI.** "TrimUI" and all product names are trademarks of their respective owners
and are used here purely to identify the hardware this firmware runs on (nominative/descriptive
use). No association or endorsement is implied.

## What's in the image, and who owns it

The firmware image is a mixture of software with different licenses. We claim **no ownership** of
any of it and add **no license of our own** to it.

- **Free / open-source components** — e.g. the **Linux kernel, U-Boot, BusyBox**, and other
  software under **GPL / LGPL / BSD / MIT / Apache** licenses (their license texts and SPDX
  identifiers are embedded in the image). These licenses **permit redistribution.**
- **Proprietary components** — TrimUI's own user-interface software and the **ARM Mali GPU
  driver**, which remain the copyright of their respective owners. These are redistributed as-is,
  unmodified, for the existing owner base of the hardware they were written for.

## GPL source-code notice (important)

This image contains **GPLv2-licensed software** (the Linux kernel, U-Boot, BusyBox, and others).
The GPL requires that the **complete corresponding source code** be made available to recipients
of the binaries.

**We do not possess that source code.** These binaries are part of a modified Allwinner BSP that
was **built and distributed by TrimUI**, who — as of this writing — has **not published** the
corresponding source. We are therefore unable to provide complete corresponding source ourselves.
The obligation to release it rests with the party that built and distributed the binaries (TrimUI).

Upstream projects for the components involved:
- Linux kernel — <https://kernel.org>
- Das U-Boot — <https://u-boot.org>
- BusyBox — <https://busybox.net>
- Allwinner BSP / community documentation — <https://linux-sunxi.org>

If TrimUI (or anyone) publishes the corresponding source, we will **link to or mirror it here on
request.** If you are a copyright holder of any component and would like your source hosted,
relayed, corrected, or your material removed, please **open an issue.**

## Takedown

If you are **TrimUI** or another authorized rights holder and you want this material taken down,
**open an issue or contact the maintainer and it will be removed promptly.** No dispute intended —
this exists only to help existing device owners.

## No warranty

Provided **AS-IS, with no warranty of any kind**, express or implied. Flashing firmware carries
risk, including the risk of rendering a device unbootable; **you assume all of that risk.** The
README explains how to revert to TrimUI's official 1.0.1 if you want to.
