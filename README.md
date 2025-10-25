# Portable Wireless Monitor (DIY)

**Status:** Parts ordered — build in progress. I will update once I test everything.

## What this is
A practical, portable second monitor you can carry and power from a power bank.  
Instead of buying a commercial model that costs $500+, this build runs about $260 (≈ ₹21,700) and is fully DIY.

The core idea: use a Raspberry Pi 4 as a small "receiver" sitting next to a portable monitor. Your laptop streams the screen to the Pi over Wi-Fi, and the Pi outputs to the monitor via HDMI. Everything runs from a power bank for real portability.

I also purchased a wireless HDMI kit as a fallback if Wi-Fi streaming is too laggy. Parts are on the way; I’ll post actual test results and tweaks after assembly.

---

## Why I built it
I often work with a single screen and that slows me down. My desk setup is cramped and I move around based on temperature in different rooms, so a lightweight, battery-powered second screen makes sense.

Off-the-shelf portable wireless monitors have issues:
- Very expensive (₹40,000+ for decent models)
- Many so-called "wireless" options still require a cable to the laptop
- Some are locked to specific ecosystems (Apple, for example)

So I decided to try a budget DIY alternative. Worst case: I spend money and learn something. Best case: a useful, portable display for about ₹22k.

---

## How it works (simple)
- Laptop has the screen content.
- Raspberry Pi 4 receives that content over Wi-Fi (VNC or another remote-display protocol).
- Pi sends video to the portable monitor over a short HDMI cable.
- The monitor and Pi share a power bank for portability.

Short cable between Pi and monitor avoids wireless problems on that link. The only wireless link is laptop <-> Pi, which both handle as full computers.

Estimated power draw and runtime (rough):
- Monitor ≈ 12 W
- Pi ≈ 15 W
- Total ≈ 27 W
With a 20,000 mAh power bank (33 W capable), expect roughly 4–6 hours of run time.

If Wi-Fi streaming shows 50–150 ms latency, the wireless HDMI kit should help; its advertised latency is in the 80–100 ms range.

---

## Parts I used (India, prices I paid — October 2025)
**Essentials**
- FRONTECH 15.6" portable monitor — ₹8,049 (Amazon)  
  - Full HD IPS, HDMI + USB-C, built-in speakers, 1-year warranty
- Raspberry Pi 4 Model B, 4 GB — ₹5,779 (Robu.in)  
  - Buy from trusted sellers (Robu.in, ElectroPi.in, Hubtronics.in)
- SanDisk 32 GB microSD (Class 10, A1) — ₹480
- Pi accessories bundle — ₹1,064 (Robu.in)
- Official Pi case — ₹306
- Micro-HDMI to HDMI cable — ₹409
- 5.1 V 3 A USB-C power supply — ₹349
- Xiaomi 20,000 mAh 33 W power bank — ₹1,899 (Amazon)
- boAt USB-C cables (100 W rated) — ₹299 each (bought two)

**Optional (backup)**
- JARNI Wireless HDMI kit — ₹3,799

**Total spent:** ₹21,668 (about $260 USD)

Notes:
- 4 GB RAM on the Pi is a good balance for this use case. 2 GB is limiting, 8 GB is unnecessary here.
- Use a quality microSD (A1-rated) for smoother performance.
- I chose Xiaomi for the power bank for reliability and price; shop trusted brands.

---

## What I originally planned (and why I changed it)
My first idea was to buy a raw LCD panel and controller and build a monitor from scratch. After reading multiple forum reports of dead panels, incompatible controllers, and other failures, I decided that route had a high failure rate for a beginner.

Instead, I bought a prebuilt portable monitor and focused on adding wireless capability. It is less "pure DIY," but much more likely to work reliably.

---

## Planned setup steps (my build plan)
> Note: this is the plan before parts arrive. I will update after testing.

### Phase 1 — Test the monitor (Day 1)
1. Connect the monitor to the laptop via HDMI.
2. Check for dead pixels, brightness, and basic functionality.
3. Return the monitor immediately if anything is wrong (7-day return window on many marketplaces).

### Phase 2 — Raspberry Pi setup (Day 2–3)
1. Download Raspberry Pi Imager to your laptop.
2. Flash Raspberry Pi OS to the microSD card.
3. Enable SSH and configure Wi-Fi during the flash (optional but saves time).
4. Put the Pi in the case, insert the microSD card.
5. Connect Pi to the monitor via micro-HDMI.
6. Power up and finish the Pi initial setup.

### Phase 3 — Enable remote display (Day 3)
1. On the Pi: `Settings → Raspberry Pi Configuration → Interfaces → Enable VNC`.
2. Note the Pi’s IP address (hover over Wi-Fi icon or check `ifconfig`).
3. Set a secure password for VNC.

### Phase 4 — Connect from laptop (Day 4)
1. Install a VNC client on the laptop (TigerVNC Viewer or similar).
2. Enter the Pi IP and the password.
3. You should see the Pi desktop in a window or fullscreen.
4. Move windows or extend your desktop as needed.

### Phase 5 — Optimize (Day 5–7)
- Tweak VNC quality and compression for better latency.
- Test typing and interactive tasks to measure perceived lag.
- If lag is unacceptable, try RDP / spacedesk / Parsec or the wireless HDMI backup.
- Sort out power distribution from the power bank and cable management.

### Phase 6 — Make it portable (Day 7+)
- Mount the Pi to the monitor (Velcro, double-sided tape, or clips).
- Pack in a laptop bag and test in different rooms to verify Wi-Fi range.

---

## Software options to stream the display
- **VNC** (default plan)  
  - Free, built into Raspberry Pi OS. Easy to set up. Typical latency 100–300 ms.
- **RDP** (Remote Desktop Protocol)  
  - Windows built-in. Latency typically 50–150 ms. Requires RDP server on Pi.
- **spacedesk** (Windows only)  
  - Makes the Pi appear as an actual second monitor to Windows. Latency ~50–100 ms.
- **Parsec**  
  - Lowest latency option in ideal cases (20–80 ms). Official Pi support was dropped in 2024, but there are community workarounds; use at your own risk.

I will try multiple options and report which one feels best for coding and general use.

---

## Lessons learned (so far)
- Wireless touch is difficult. Touch input travels over USB, not over the video stream. Wireless USB extenders exist but user reports are poor. If touch is required, the touch USB must be wired to the Pi, which removes the "full wireless" aspect.
- Building from raw panels has a high chance of failure for beginners. Starting with a prebuilt portable monitor saves time and reduces risk.

---

## Future notes
- I will post test results after I finish assembly and try the Wi-Fi and wireless HDMI options.
- If you want to replicate this, follow the parts list and the setup phases. I’ll include exact commands and configuration tweaks in a follow-up commit.

---

## License
This is my personal project documentation. Use and adapt freely for non-commercial purposes. If you reproduce this, attribution is appreciated.

