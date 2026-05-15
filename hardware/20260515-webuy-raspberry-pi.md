# WeBuy Portugal — SBC Hardware Research
**Date:** 2026-05-15
**Source URLs:**
- https://pt.webuy.com/product-detail/?id=SSOBBANPIBPIM5C
- https://pt.webuy.com/product-detail/?id=SSOBRASPI3BB
- https://pt.webuy.com/product-detail/?id=SSOBRASPI3BC
- https://pt.webuy.com/product-detail/?id=SDESORAPI3LTS89B

**Context:** Evaluating secondary SBC nodes to expand a home lab that already runs a Raspberry Pi 5 in production.

---

## CeX Grading Reference
- **A** — Like new, complete, may have very minor marks
- **B** — Good condition, fully working, visible wear or light scratches
- **C** — Heavy wear/scratches, fully working but cosmetically rough

---

## Products

### 1. Banana Pi BPI-M5 — Grade C
**ID:** SSOBBANPIBPIM5C
**Buy price:** €45.00
**Sell back:** €20 cash / €26 voucher
**Condition:** C (significant cosmetic wear)
**In stock online:** Yes

**Specs:**
- SoC: Amlogic S905X3 quad-core Cortex-A55 @ 1.8GHz
- RAM: 4GB LPDDR4
- Storage: 16GB eMMC
- USB: 4x USB 3.0 + 1x USB-C OTG
- Network: Gigabit Ethernet (no built-in WiFi)
- Video: HDMI 2.0 (4K)
- GPIO: 26-pin header
- OS support: Android, Ubuntu, Debian, Armbian

**Verdict:** SKIP
Grade C on an SBC is a real risk — could mean damaged GPIO pins, bent ports, or corrosion. The 4GB RAM and Amlogic S905X3 are appealing for a media/Docker node, but €45 is not a meaningful discount over new (~€60) given the unknown physical state. Do not put anything important on this.

---

### 2. Raspberry Pi 3 Model B — Grade B
**ID:** SSOBRASPI3BB
**Buy price:** €35.00
**Sell back:** €19 cash / €23 voucher
**Condition:** B (good, some visible wear)
**In stock online:** Yes

**Specs:**
- SoC: Broadcom BCM2837 ARMv8 quad-core @ 1.2GHz (64-bit)
- RAM: 1GB LPDDR2
- Storage: MicroSD only (no eMMC)
- USB: 4x USB 2.0
- Network: 100Mbps Ethernet, 802.11n WiFi, Bluetooth 4.1 BLE
- Video: Full HDMI
- GPIO: 40-pin header, CSI, DSI, composite audio/video

**Verdict:** SKIP
€35 is expensive for a 2016-era board in 2026. Only 1GB RAM and 100Mbps Ethernet make it a weak secondary node. The Orange Pi 3 LTS (below) gives you 2GB RAM, Gigabit, and eMMC for €3 less. The only reason to choose this over alternatives is existing RPi ecosystem knowledge or need for the specific GPIO/camera interface support.

---

### 3. Raspberry Pi 3 Model B — Grade C
**ID:** SSOBRASPI3BC
**Buy price:** €30.00
**Sell back:** €16 cash / €20 voucher
**Condition:** C (heavy wear)
**In stock online:** Yes

**Specs:** Same as #2 above.

**Verdict:** HARD SKIP
Same board as above, worse condition, only €5 cheaper. Not worth it at any price when better alternatives exist in this range.

---

### 4. Orange Pi 3 LTS 2GB RAM 8GB eMMC — Grade B
**ID:** SDESORAPI3LTS89B
**Buy price:** €32.00
**Sell back:** €14 cash / €18 voucher
**Condition:** B (good, some visible wear)
**In stock online:** Yes

**Specs:**
- SoC: Allwinner H6 quad-core Cortex-A53 @ 1.8GHz
- RAM: 2GB LPDDR4
- Storage: 8GB eMMC (no SD card needed for boot)
- USB: 2x USB 3.0, 1x USB 2.0
- Network: Gigabit Ethernet
- Video: HDMI 2.0
- GPIO: 26-pin header
- LTS: Long-Term Support kernel and OS support

**Verdict:** BEST OF THE FOUR — worth considering
Double the RAM of the RPi 3, Gigabit instead of 100Mbps, and built-in eMMC for reliability (SD cards fail; eMMC does not). The LTS designation means Orange Pi commits to long-term kernel/OS support — good for a node you set up and forget. Grade B condition is acceptable. €32 is fair. Good candidates for this board: Pi-hole/AdGuard Home, Grafana/Netdata node, MQTT broker, secondary DNS, lightweight automation.

**Limitations:** Smaller community than RPi, fewer prebuilt images, some peripherals may need manual driver work.

---

## Final Recommendation

**Buy:** Orange Pi 3 LTS (€32, Grade B) — if you want a cheap utility node to offload lightweight services from the RPi 5.

**Skip:** Everything else.
- RPi 3 boards are overpriced relics for what they deliver in 2026.
- Banana Pi M5 is interesting on paper but Grade C condition is a gamble for electronics.

**Important:** None of these should replace or mirror the RPi 5 for production workloads. Treat them as dedicated single-purpose nodes (DNS, monitoring, IoT gateway) and keep production on the Pi 5.

If the goal is more compute, save up for a second RPi 5 or look at an N100 mini PC — more headroom for roughly €80-120 secondhand.
