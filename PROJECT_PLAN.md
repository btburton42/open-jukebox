# Project DAP-Galaxy: Implementation Plan

## Project Overview
Transform Samsung Galaxy smartphones (S8-S10, Note series) into dedicated, high-fidelity digital audio players (DAPs) using a custom AOSP-based ROM.

---

## Phase 1: Hardware Acquisition & Preparation
**Timeline:** Week 1-2
**Status:** Pending

### Tasks
- [ ] Source 2-3 Exynos-variant Galaxy devices (F/FD/N models)
  - Preferred: S10+ or Note 10 for battery life
  - Avoid: US/Canadian Snapdragon variants (U/U1/W)
- [ ] Verify bootloader unlock capability
- [ ] Document Knox bit status before flashing
- [ ] Acquire USB-C DAC for testing (if using external audio)

### Deliverables
- [ ] Hardware inventory spreadsheet
- [ ] Knox status documentation
- [ ] Test device setup

---

## Phase 2: Base ROM Development
**Timeline:** Week 3-5
**Status:** Pending

### Tasks
- [ ] Download and configure LineageOS for MicroG (Android 13/14)
- [ ] Build custom ROM image for target devices
- [ ] Test MicroG integration for Apple Music compatibility
- [ ] Verify Widevine L3 functionality
- [ ] Create automated build pipeline

### Deliverables
- [ ] Custom ROM images (per device variant)
- [ ] Build documentation
- [ ] Flashing instructions

---

## Phase 3: System Debloating & Optimization
**Timeline:** Week 6-7
**Status:** Pending

### Tasks
- [ ] Create ADB debloat script for package removal
  - Remove: com.android.phone, com.android.telephony, com.android.messaging
  - Remove: com.android.camera2, com.android.contacts, com.android.calendar
  - Remove: com.android.browser, com.android.email
- [ ] Test system stability after debloating
- [ ] Optimize battery settings (Naptime integration)
- [ ] Configure aggressive doze mode

### Deliverables
- [ ] `debloat.sh` - ADB script for package removal
- [ ] System stability test results
- [ ] Battery optimization profile

---

## Phase 4: Audio Pipeline Integration
**Timeline:** Week 8-9
**Status:** Pending

### Tasks
- [ ] Integrate JamesDSP as system-level driver
- [ ] Configure parametric EQ presets
- [ ] Test convolution filter support
- [ ] Verify UAC2 USB DAC compatibility
- [ ] Map Bixby button to Play/Pause/Next Track
- [ ] Test bypassing Android resampling (48kHz)

### Deliverables
- [ ] JamesDSP configuration files
- [ ] EQ preset library
- [ ] USB DAC compatibility matrix
- [ ] Button mapping utility

---

## Phase 5: Security & DRM Bypass
**Timeline:** Week 10-11
**Status:** Pending

### Tasks
- [ ] Integrate KernelSU (kernel-level root)
- [ ] Configure KernelSU to hide su from userspace
- [ ] Install Play Integrity Fix (PIF) module
- [ ] Test Apple Music DRM validation
- [ ] Verify subscription checks pass
- [ ] Document security trade-offs

### Deliverables
- [ ] KernelSU configuration
- [ ] PIF module setup guide
- [ ] Apple Music compatibility test results

---

## Phase 6: User Interface Customization
**Timeline:** Week 12-13
**Status:** Pending

### Tasks
- [ ] Install and configure Olauncher/Niagara Launcher
- [ ] Create text-only, distraction-free layout
- [ ] Set up app pinning for Apple Music kiosk mode
- [ ] Configure boot-to-music workflow
- [ ] Test accessibility features

### Deliverables
- [ ] Launcher configuration backup
- [ ] UI/UX documentation
- [ ] User guide

---

## Phase 7: Integration & Testing
**Timeline:** Week 14-16
**Status:** Pending

### Tasks
- [ ] End-to-end system testing
- [ ] Audio quality verification (frequency response, THD)
- [ ] Battery life testing (idle vs. playback)
- [ ] Thermal management testing
- [ ] Stress testing (72-hour continuous playback)
- [ ] Document known issues and limitations

### Deliverables
- [ ] Test report
- [ ] Performance benchmarks
- [ ] Troubleshooting guide

---

## Phase 8: Documentation & Release
**Timeline:** Week 17-18
**Status:** Pending

### Tasks
- [ ] Write comprehensive flashing guide
- [ ] Create video tutorials
- [ ] Document hardware recommendations
- [ ] Create FAQ
- [ ] Package ROM images and scripts
- [ ] Publish release notes

### Deliverables
- [ ] `FLASHING_GUIDE.md`
- [ ] Video tutorials
- [ ] Packaged release artifacts
- [ ] GitHub release

---

## Technical Requirements

### Hardware
- Samsung Galaxy S8/S9/S10/Note (Exynos variants)
- USB-C cable
- Optional: External USB DAC
- Computer with ADB/fastboot

### Software
- LineageOS for MicroG
- KernelSU
- JamesDSP/ViPER4Android
- Olauncher/Niagara Launcher
- Play Integrity Fix
- Naptime (battery optimization)

### Tools
- Android SDK Platform Tools
- Heimdall/Odin (Samsung flashing)
- Python 3.x (for automation scripts)
- Git

---

## Risk Assessment

| Risk | Impact | Mitigation |
|------|--------|------------|
| Knox bit trigger | Permanent Samsung feature loss | Document clearly; accept as trade-off |
| Widevine L1 downgrade | Video quality only | Audio unaffected; document limitation |
| Apple Music blocking | Core functionality failure | Implement PIF; test thoroughly |
| Bootloop | Device unusable | Keep stock ROM backups; test incrementally |
| Battery degradation | Reduced playback time | Test battery health; recommend new devices |

---

## Success Criteria

- [ ] Apple Music streams Lossless/Hi-Res audio successfully
- [ ] No smartphone distractions (calls, texts, notifications)
- [ ] 10+ hour continuous playback battery life
- [ ] System-wide EQ/DSP functioning
- [ ] Boot-to-music in <30 seconds
- [ ] Stable operation for 72+ hours

---

## Next Steps

1. **Immediate:** Source test hardware (Exynos Galaxy devices)
2. **Week 1:** Begin ROM compilation and testing
3. **Week 3:** Start development of debloat script
4. **Week 6:** Audio pipeline integration

---

*Last Updated: 2026-03-28*
*Version: 1.0*
