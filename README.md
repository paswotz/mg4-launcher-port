<img width="1200" height="630" alt="MG4 Launcher" src="https://github.com/user-attachments/assets/dffe6036-0249-4888-9154-9af12c313e1e" />

<div align="center">

# SAIC MG4 Launcher Port (Experimental)

### Experimental compatibility builds for running the newest SAIC MG launcher on older MG4 headunits

![Status](https://img.shields.io/badge/status-experimental-orange?style=for-the-badge)
![Android](https://img.shields.io/badge/android-9%20%2F%20API%2028-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Platform](https://img.shields.io/badge/platform-MG%20%2F%20SAIC-1f6f3f?style=for-the-badge)
![Builds](https://img.shields.io/badge/builds-model--specific-blue?style=for-the-badge)

</div>

---

## 🚘 Project Overview

This community project focuses on porting MG's latest launcher. By patching the new launcher, we enable it to be installed directly as an update over the legacy version.

Status legend for MG4 models:

- 🟢 The launcher can be used for daily use.
- 🟡 The launcher can be used, but still has unresolved bugs.
- 🟠 The launcher starts but is not functional.
- 🔴 The launcher can not be used.

> [!IMPORTANT]  
> These are experimental test builds. Use only the APK that matches the tested model group.

---

## 📊 Current Model Status

Status | Model | Error | Known Issues | Release APK
| --- | --- | --- | --- | --- |
| 🟠 | **SWI168** |  **Starts with UI but without services** | The launcher's user interface does not dynamically adapt to different screen sizes or resolutions yet. System services such as battery status, location tracking, and device telemetry currently return null values. | [`launcher_swi168_v1.apk`](https://github.com/paswotz/mg4-launcher-port/releases/download/v1/launcher_swi168_v1.apk)
| 🟠 | **SWI165** | **Starts with UI but without services** | The launcher's user interface does not dynamically adapt to different screen sizes or resolutions yet. System services such as battery status, location tracking, and device telemetry currently return null values. | [`launcher_swi165_v1.apk`](https://github.com/paswotz/mg4-launcher-port/releases/download/v1/launcher_swi165_v1.apk)
| 🔴 | **SWI133** | **Launcher crashes on startup** | The launcher currently fails to boot and crashes immediately during the startup sequence. | [`launcher_swi133_v1.apk`](https://github.com/paswotz/mg4-launcher-port/releases/download/v1/launcher_swi133_v1.apk)

---

## 🛠️ Patch Summary

| Area | Patch | Reason |
| --- | --- | --- |
| 🔐 Package install | Removed `sharedUserId` | Allows installation as an update on tested target systems. |
| 🔢 Versioning | Raised `versionCode` / `versionName` | Ensures Android recognizes the APK as newer than the system launcher. |
| ✍️ Signing | Signed with available Android platform key | Required for privileged/system-style launcher update testing. |
| 🚗 CPAA service | Disabled unavailable CPAA service initialization | Prevents repeated attempts to start missing `com.saicmotor.projection.service.CpaaService`. |
| 🪵 Diagnostics | Added internal logcat collector to diagnostic builds | Copies `mce25_launcher_diag_*.log` to USB / Download where possible. |
| 🧪 SWI165 UI debug | Added visible green overlay | Separates "Activity is not visible" from "launcher content is empty". |

---

## ✨ Contribution & Support

- Thanks to [`SliDeeN`](https://github.com/SliDeeN) for his great app [`MG4Control`](https://github.com/SliDeeN/MG4Control) and testing on SWI133
- Thanks to [`suchhodler-boop`](https://github.com/suchhodler-boop) (XDA: `FrAsErTaG`) for testing on SWI165
- Thanks to `san-sai` (XDA) for testing on SWI168

> [!TIP]
> **Want to join and support the project?**  
> Feel free to drop me a private message on **[XDA](https://xdaforums.com/m/kruemelmonster96.13293805/)** letting me know which **MG4 model** you drive!

---

## ⚠️ Safety Notice

These APKs are **test builds for controlled debugging**. They may bypass or disable parts of the original launcher behavior while isolating compatibility problems.

Always keep a way to uninstall the update or restore the original system launcher state.
