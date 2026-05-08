# pkgbuild-mechrevo-driver-dkms-16-pro
Modified version of [tuxedo-drivers](https://gitlab.com/tuxedocomputers/development/packages/tuxedo-drivers). Tested on MECHREVO JIAOLONG Series 16 Pro 2025 (9955HX).

For modification, see [patch.diff](patch.diff) file. Inspired from [commit 26d2f1c](https://github.com/nanomatters/tuxedo-drivers/commit/26d2f1cb31e186d7e225327afe0cb33ab5cc8938#diff-7415c9e2ade65a61f5dc8ce903ae2d82f7979a9ef9a685a63eb63311e5a190cd) for XMG NEO 16 A25. In theory, any uniwill devices that use motherboard codename `X6FR57TK` (Uniwill IDY/IDK) (XMG NEO 16 A25, XMG APEX 16 MAX M25 (9955HX), MECHREVO JIAOLONG 16 Pro/CANGLONG 16 Ultra/XPro) is supported by upstream and can be supported with similar modification. `X6FR57TK-B2` (8945HX) is not tested, use with caution.

Features in tuxedo-control-center that verified to working: Fan control, CPU power limit (PL1, PL2, PL4), CPU frequency control, NVIDIA cTGP, Keyboard backlight, Battery charge options.

Based on original pkgbuild, dkms.conf and patch.diff file from [Shiina Rikka (RikkaNekoo)](https://github.com/RikkaNekoo)'s AUR package [mechrevo-drivers-dkms](https://aur.archlinux.org/packages/mechrevo-drivers-dkms).

## Warning for DrMOS high tempture on 2025 Uniwill devices

Lots of laptops using uniwill ODM design (for example, all laptops mentioned above) are known for dangerously high CPU VRM DrMOS tempture.

On uniwill IDK, it's observed CPU VDDCR_VDD VRM tempture gets 98-105 degree Celsius with 125-140A CPU Core Current load, where on uniwill IDY this tempture reached 110~120 degree Celsius.

For most DrMOS, the absolute maximum temperture is at 125 degree Celsius. Quote warning from datasheet:

**Stresses beyond those listed in this section can cause permanent damage to the device. Exposure to absolute maximum rating conditions for extended periods may affect device reliability.**

Thus, it's strongly recommended to **limit CPU power to 80W** on those device, and replace stock thermal putty as soon as possible.

(For X6FR57TK, there are 6 phases of MPS CD75101 DrMOS, which current capability is rated to 35A@25c and 20A@100c each phase. Current load>20A will leads to excessive overheat on these DrMOS.)
