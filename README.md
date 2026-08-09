# 🚀 sandybridge-android
> **Pure Android 11 (AOSP) for Legacy Intel Sandy Bridge Architecture with Native Hardware Acceleration & GSI Support**  
> *Powered by Project Celadon & Open-Source Mesa3D (Crocus/i965)*

---

## 📌 Overview

`sandybridge-open` is a targeted, open-source Android 11 build tree specifically patched and optimized for **2nd Gen Intel Core Processors (Sandy Bridge)** and **Intel HD Graphics 3000 (Gen6 GPU)**.

Most modern x86 Android and Intel Celadon builds target newer microarchitectures (Silvermont, Haswell, Kaby Lake). As a result, C/C++ compilers routinely inject instruction sets like `MOVBE` or `AVX2` into core system libraries. On Sandy Bridge hardware, this causes instant **`SIGILL` (Illegal Instruction)** crash loops in `libart`, `surfaceflinger`, and `Mesa3D`.

This project strips out unsupported x86 instruction leaks at the compiler level while preserving **full OpenGL ES hardware acceleration** through open-source Mesa drivers.

---

## ✨ Key Features

* ⚙️ **Pure Sandy Bridge Target (`-march=sandybridge`):** Zero `MOVBE` / Zero `AVX2` instruction leaks. 100% stable userspace binaries (`libart`, `surfaceflinger`, `libcrypto`).
* 🎨 **Native Hardware Acceleration:** Full GLES 2.0 / SurfaceFlinger HW acceleration via open-source Mesa3D (`crocus` / `i965` HAL stack) for Intel HD Graphics 3000.
* 🧩 **GSI & Treble Ready:** Includes vendor-in-system boundaries and target framework bounds for x86_64 Generic System Image (GSI) testing.
* 🛡️ **CPUID Fallback Protection:** Integrated Mesa3D graphics pipeline built with strict feature checking to prevent user-space GPU driver crashes.
* ⚡ **Optimized LLVM/Clang Pipeline:** Built with Soong/Ninja build system utilizing global CFLAG overrides.

---

## 🛠️ Build Configuration Snippet

If you are compiling this source tree locally, make sure your target architecture flags in `BoardConfig.mk` / `device.mk` match the following profile:

```make
# Target Architecture Overrides
TARGET_ARCH := x86_64
TARGET_ARCH_VARIANT := sandybridge
TARGET_CPU_ABI := x86_64
TARGET_CPU_ABI2 := x86
