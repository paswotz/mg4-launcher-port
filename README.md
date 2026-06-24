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

This project investigates whether the newest **MG Launcher** can be installed as an update over older MG4 launcher builds.

Status legend for MG4 models:

- 🟢 The launcher can be used for daily use.
- 🟡 The launcher can be used, but still has unresolved bugs.
- 🔴 The launcher can not be used.

> [!IMPORTANT]  
> These are experimental test builds. Use only the APK that matches the tested model group.

---

## 📊 Current Model Status

Status | Model | Error | Description | Release APK
| --- | --- | --- | --- | --- |
| 🔴 | **SWI168** |  **Starts with black screen** | Installs and reaches `MainActivity.onResume`. No launcher crash seen in logs. CPAA service loop is patched out. |
| 🔴 | **SWI165** | **Starts with black screen** | Active debug build with visible green `SWI165 UI DEBUG` overlay. Used to confirm whether the Activity renders or the content path stays empty. |
| 🔴 | **SWI133** | **Launcher crashes on startup** | Built for the early `ClassNotFoundException` / `CoreComponentFactory` startup crash path. Does not include the diagnostic logcat collector. |

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

## 🔍 Findings From Logs

### ✅ Confirmed

- The MCE25 launcher can be installed as an update on tested systems.
- On SWI168 and SWI165 logs, the launcher process starts and reaches `MainActivity`.
- The CPAA service is missing on some R67 / EH32 systems.
- The CPAA loop is fixed in the CPAA-patched builds.

### ⚠️ Still under investigation

- SWI165 currently starts but still shows a black screen for the tester.
- `com.custom.launcher` / Nova-style components can regain HOME focus and pause the SAIC launcher.
- `com.saicmotor.mapservice` errors appear in some logs. These are not launcher crashes, but may explain missing navigation/content cards.

---

## 🧪 Tester Workflow

1. Pick the APK for the exact model group.
2. Install it as an update over the existing SAIC launcher.
3. Set **SAIC Launcher** as default HOME if Android asks.
4. Launch it and wait **10-15 seconds** without pressing HOME or the side bar.
5. For SWI165, check whether the green **`SWI165 UI DEBUG`** overlay is visible.
6. Send back all generated `mce25_launcher_diag_*.log` files from USB or Download.

> [!TIP]  
> If the SWI165 overlay is visible, the Activity is rendering and the remaining bug is likely inside the launcher content / fragment / data-provider path.  
> If the overlay is not visible, the next area to inspect is HOME focus, SystemUI window behavior, or activity visibility.

---

## 🗂️ Repository Layout

```text
MCE25/
├── README.md
├── swi133/
│   └── launcher_mce25_r67_crashfix1_signed.apk
├── swi165/
│   ├── launcher_mce25_r67_swi165_cpaa1_signed.apk
│   └── launcher_mce25_r67_swi165_ui_debug1_signed.apk
└── swi168/
    └── launcher_mce25_r67_cpaa1_signed.apk
```

---

## 🧭 Roadmap

- [ ] Confirm whether the SWI165 debug overlay is visible on the tester vehicle.
- [ ] If visible: patch the launcher content / fragment path.
- [ ] Add guards for missing map, navigation, and provider data.
- [ ] Keep SWI133, SWI165, and SWI168 builds separate until compatibility differences are fully understood.
- [ ] Merge model-specific fixes only after repeated logs confirm the same behavior.

---

## ⚠️ Safety Notice

These APKs are **test builds for controlled debugging**. They may bypass or disable parts of the original launcher behavior while isolating compatibility problems.

Always keep a way to uninstall the update or restore the original system launcher state.
