# WeBuy Portugal — SBC Hardware Research
**Date:** 2026-05-15
**Source URLs:**
- https://pt.webuy.com/product-detail/?id=SSOBBANPIBPIM5C
- https://pt.webuy.com/product-detail/?id=SSOBRASPI3BB
- https://pt.webuy.com/product-detail/?id=SSOBRASPI3BC
- https://pt.webuy.com/product-detail/?id=SDESORAPI3LTS89B

**Additional reference:** https://blog.alexellis.io/n100-mini-computer/ (Alex Ellis, Aug 2025)

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
- Geekbench 6 (for reference, RPi 4 is ~291/657; RPi 3 is slower)

**Verdict:** SKIP
€35 is expensive for a 2016-era board in 2026. Only 1GB RAM and 100Mbps Ethernet make it a weak secondary node. The Orange Pi 3 LTS (below) gives you 2GB RAM, Gigabit, and eMMC for €3 less. The only reason to choose this over alternatives is existing RPi ecosystem knowledge or need for specific GPIO/camera interface support.

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

## Alternative Context: Intel N100 Mini PC

> Source: Alex Ellis — "I Bought An N100 Mini PC, Then Another" (Aug 2025)
> https://blog.alexellis.io/n100-mini-computer/

This section was added to provide a realistic upper-bound comparison for anyone considering spending more for actual compute.

### What it is
The Intel N100 is a fanless 4-core/4-thread x86 processor with max turbo at 3.4GHz. It ships inside compact "mini PC" or "fanless router" enclosures, typically with 4x 2.5Gbps Ethernet ports, full-size HDMI, NVMe boot drive support, and KVM virtualisation. Power supply is included.

### Pricing (new, as of 2025)
- Bare-bones unit: ~£130 / ~€155
- 32GB DDR5 RAM (Crucial): ~£65 / ~€78
- NVMe SSD (1TB, e.g. Crucial P3 Plus): ~£65 / ~€78
- **Total fully loaded: ~£260 / ~€310**

Pre-populated configs (OEM RAM + smaller NVMe) are available cheaper. Look for **i226-V** NIC for stable networking.

### Performance — Geekbench 6 (single-core / multi-core)
| Device | Single | Multi |
|--------|--------|-------|
| Raspberry Pi 4 | 291 | 657 |
| Raspberry Pi 5 | 777 | 1,496 |
| **Intel N100** | **1,226** | **3,345** |
| AMD Ryzen 9 5950X | 2,075 | 10,735 |
| Acemagic F3A (AMD AI 9) | 2,454 | 11,365 |

The N100 is **1.6x faster single-core and 2.2x faster multi-core than a Raspberry Pi 5** — and supports KVM, which the RPi 5 does not. Alex ran 3x Firecracker microVMs on a single N100 at roughly the cost of one fully kitted RPi 5 16GB.

### Heat
Fanless = silent, but it gets hot. Idle: CPU ~45°C, NVMe ~56°C. Under a 3-node K3s workload: CPU ~55°C, NVMe ~61°C. Direct sunlight pushed NVMe to 85–90°C. Avoid direct sun; consider ventilation. Some users add external PC fans over the heatsinks.

### Use cases validated by Alex Ellis
- 3x Firecracker/KVM microVMs simultaneously
- K3s multi-node clusters
- GitHub Actions runners (via actuated)
- Headless Ubuntu LTS server, SSH-only
- Docker workloads, benchmarking, burn-in testing

### Verdict
If you need real compute — containers, VMs, Kubernetes, CI runners — the N100 is the right tool. It outperforms a RPi 5 significantly, supports KVM virtualisation, and at ~€155 bare-bones is surprisingly affordable for what it delivers. Budget ~€300 for a fully loaded config.

Not a fit if you need GPIO, low idle power draw (<6W), or ARM-native builds. Also not secondhand-available on WeBuy PT at this time.

---

## Final Recommendation

### If your budget is €30–45 (WeBuy only)
**Buy:** Orange Pi 3 LTS (€32, Grade B) — best of the four WeBuy listings. Use it as a dedicated lightweight node: Pi-hole, AdGuard, MQTT broker, Netdata, secondary DNS.

**Skip:** Everything else on this list. RPi 3 boards are overpriced for 2016 hardware. Banana Pi M5 at Grade C is a gamble.

### If your budget is €150–310 (new hardware)
**Consider:** Intel N100 mini PC. Buy bare-bones (~€155) and add your own RAM + NVMe. It runs circles around anything in the WeBuy list, supports KVM/Firecracker, and can host an entire microVM cluster. This is the "one machine to rule them all" for a serious home lab addition.

### What none of these should do
Replace or mirror the RPi 5 for production services. The RPi 5 stays as the production node. These are utility/experiment additions only.
