# AERA Recovery for Redmi Note 10 5G (camellia) — first MediaTek port

Unofficial, experimental device tree bringing [AERA Recovery](https://github.com/AERA-Recovery)
to the Xiaomi Redmi Note 10 5G / Note 10 5G Global (camellia / camellian, MediaTek MT6833).
Every AERA device before this one is Snapdragon — this is the first MediaTek port attempt.

**Maintainer:** hisvoice · **Status:** Beta / bring-up · **AERA branch:** aera-16.0

## Bootstrap layout (temporary)

For the first build, the device tree ships as **`tree.zip`** at this repo's root;
the build workflow unpacks it into `device/xiaomi/camellia` inside the AERA source.
The zip will be expanded into a regular file tree in a later cleanup — the tree
contents are identical either way.

## Building

GitHub Actions → **Build AERA Recovery (Android 16)** → Run workflow
(defaults: `camellia`, `device/xiaomi/camellia`, `bootimage`).
Output `boot.img` is published to a release tagged `AERA-camellia-<run id>`.
Flash to **boot** (camellia is virtual A/B, recovery-as-boot; there is no recovery partition):
`fastboot flash boot boot.img`

## Honest status

- Decryption (FBE, Microtrust TEE): **unproven** — first build's open question.
- Touch: Novatek + FocalTech firmware included; the donor backlight-poll wake
  watchdog from the camellia TWRP work is carried in.
- **Not supported in this port:** SIM mobile data in recovery (AERA's modem
  features are Qualcomm-based) and Wi-Fi in recovery (no MTK connectivity
  stack in the recovery ramdisk, v1).
- Root Manager module catalog is disabled: it targets GKI kernels (6.x KMI);
  camellia runs a 4.14 non-GKI kernel.

Keep a stock boot.img from your current ROM handy before flashing — it is the
one-command way back.
