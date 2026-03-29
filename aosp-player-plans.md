Here is the compiled research and technical specification for **Project DAP-Galaxy**. This document is structured for ingestion by a development agent to begin the architecture of a dedicated music-only AOSP fork.

## **Project DAP-Galaxy: Technical Specification & Implementation Guide**

### **1\. Target Hardware & Bootloader Constraints**

Samsung devices require specific handling due to the Knox security suite and chipset variations.

* **Preferred Models:** Galaxy S8, S9, S10, and Note equivalents.  
* **Chipset Architecture:** Prioritize **Exynos** variants (F/FD/N models). These typically have unlockable bootloaders, whereas US/Canadian Snapdragon variants (U/U1/W) are often hard-locked, preventing custom AOSP installation.  
* **The Knox Trigger:** Document that flashing custom firmware will trip the **Knox bit (0x1)**. This is a one-way hardware fuse that disables Samsung-specific security features (Pay, Secure Folder), which is acceptable for a dedicated audio appliance.

### **2\. AOSP Base & Compatibility Layer**

To ensure Apple Music functions without a full Google suite, the base ROM must handle micro-services efficiently.

* **Base ROM:** **LineageOS for MicroG** (Android 13 or 14).  
* **The MicroG Requirement:** Apple Music relies on Google Play Services for subscription validation and Widevine DRM. MicroG provides these APIs with a significantly smaller footprint and lower background CPU usage.  
* **DRM Status:** Note that unlocking the bootloader usually downgrades the device to **Widevine L3**. While this affects video resolution, it generally allows for Lossless/Hi-Res audio streaming in Apple Music.

### **3\. The "Music-Only" Environment**

The goal is to eliminate all "smartphone" distractions and background processes.

* **Headless Debloating:** Utilize a post-flash shell script to remove non-essential packages:  
  * com.android.phone, com.android.telephony, com.android.messaging (Kill cellular standby).  
  * com.android.camera2, com.android.contacts, com.android.calendar.  
  * com.android.browser, com.android.email.  
* **Minimalist UI:** Set a "Kiosk" launcher as the default.  
  * **Olauncher** or **Niagara Launcher** are recommended for a text-based, distraction-free interface.  
  * Use **App Pinning** (*Settings \> Security*) to lock the device into the Apple Music interface upon boot.

### **4\. Audio Signal Path & DSP Integration**

Standard Android often resamples audio to 48kHz. This specification aims to bypass or optimize that path.

* **DSP Engine:** Integrate **JamesDSP** or **ViPER4Android** as system-level drivers. This allows for system-wide parametric EQ, convolution filters, and crossfeed.  
* **USB Audio:** If using an external DAC, ensure the kernel supports **USB Audio Class 2 (UAC2)**.  
* **Hardware Mapping:** Map the physical "Bixby" button (if present) to a global Play/Pause or Next Track command using a key mapper.

### **5\. Security & Integrity Strategy**

Apple Music performs several checks to prevent running on compromised devices.

* **Root Solution:** Use **KernelSU** instead of Magisk.  
  * *Why:* KernelSU operates at the kernel level, making the su binary invisible to userspace apps by default.  
* **Integrity Spoofing:** If Apple Music refuses to boot, include the **Play Integrity Fix (PIF)** module to mask the unlocked bootloader status.  
* **Battery Optimization:** Use **Naptime** or a similar aggressive doze script to ensure the device consumes near-zero power when not playing music.

### **Summary of Build Components**

| Category | Component | Technical Note |
| :---- | :---- | :---- |
| **OS Core** | LineageOS \+ MicroG | Minimizes background telemetry. |
| **Root** | KernelSU | Essential for hiding root from Apple Music. |
| **DSP** | JamesDSP | Best-in-class system-wide audio processing. |
| **UI** | Olauncher | Text-only minimalist launcher. |
| **Security** | Play Integrity Fix | Required for DRM/Subscription verification. |

Would you like me to generate a **Python-based ADB debloat script** that lists the specific system packages you should target for removal from these Samsung models?