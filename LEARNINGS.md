# DAP-Galaxy Project Learnings

## Hardware Requirements Discovered

### Samsung Galaxy S9 Model Variants

**Compatible (Exynos - can unlock bootloader):**
- SM-G960F (International Single SIM)
- SM-G960FD (International Dual SIM)  
- SM-G960N (Korea)

**Incompatible (Snapdragon - permanently locked):**
- SM-G960U (US Carrier)
- SM-G960U1 (US Unlocked) ← **User's current device**
- SM-G960W (Canada)
- SM-G9600 (China)

### Why Snapdragon Models Don't Work

US/Canadian Snapdragon variants have **hardware-fused bootloaders** that cannot be unlocked:
- OEM unlock option missing from Developer Settings
- Samsung Knox security at hardware level
- No known bypass methods
- Even if "OEM unlock" toggle appears, it won't actually unlock

### Verification Method

Download Mode (Vol Down + Bixby + Power) shows:
- **Locked:** "CURRENT BINARY: Samsung Official" + "SECURE DOWNLOAD: ENABLE"
- **Unlocked:** "OEM LOCK: OFF" (missing from user's screenshot)

## Project Status

- ✅ Project plan created (18-week roadmap)
- ✅ Hardware research completed
- ❌ User's device incompatible (SM-G960U1)
- 🔲 Need to source Exynos variant

## iPhone SE (1st gen) Assessment

**Verdict: NOT COMPATIBLE**

Reasons:
- iOS bootloader permanently locked by Apple
- No custom ROM support (no LineageOS, no AOSP)
- Cannot flash alternative operating systems
- Project requires Android device with unlockable bootloader

## Required Device Characteristics

To build a custom AOSP music player, device MUST have:
1. **Unlockable bootloader** (OEM unlock in Developer Options)
2. **Custom ROM support** (LineageOS or similar)
3. **Android-based** (AOSP is Android Open Source Project)
4. **3.5mm headphone jack** (or USB-C DAC support)

## Recommendations

1. Source SM-G960F/FD/N from eBay/Marketplace (usually $50-100)
2. Verify seller provides "OEM unlock" confirmation or accept returns
3. Check XDA forums for device-specific unlocking guides before purchase
4. Alternative: Any Android phone with official LineageOS support
