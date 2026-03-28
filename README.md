<div align="center">

# 🖥️ ZXC.AIDA

**Native Windows hardware monitoring and system diagnostics utility built with WinUI 3**

[![Platform](https://img.shields.io/badge/platform-Windows%2010%20%7C%2011-0078D4?style=flat-square&logo=windows)](https://microsoft.com/windows)
[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square&logo=dotnet)](https://dotnet.microsoft.com/)
[![UI](https://img.shields.io/badge/UI-WinUI%203-005FB8?style=flat-square&logo=windows)](https://learn.microsoft.com/en-us/windows/apps/winui/winui3/)
[![Lang](https://img.shields.io/badge/lang-en%20%7C%20ru-grey?style=flat-square)](#-localization)
[![License](https://img.shields.io/badge/license-proprietary-red?style=flat-square)](#)

---

A desktop hardware monitoring application for Windows 10 and Windows 11.
Fast startup · Low overhead · Real-time telemetry · Calm, Windows-native interface.

</div>

---

## 📖 Overview

ZXC.AIDA combines **hardware inventory**, **live system telemetry**, **sensor surfaces**, **process insights**, and **troubleshooting tools** in a single Windows desktop application — without the weight of Electron or browser-based dashboards.

<br>

## ✨ Features

| Area | Capabilities |
|---|---|
| **CPU** | Identity, live per-core utilization |
| **GPU** | Inventory, live utilization, VRAM, clocks, power, PCIe link info, NVIDIA telemetry via `nvidia-smi` |
| **Memory** | Usage breakdown, physical module (DIMM) inventory |
| **Storage** | Throughput, drive inventory, Windows storage temperature paths |
| **Network** | Throughput, adapter inventory, built-in speed-test surface |
| **Processes** | Live activity list with filtering and sorting |
| **Sensors** | Unified sensor views with human-readable names and explanations |
| **Diagnostics** | Support bundle export, structured logging, localization, theme handling |

<br>

## 🎯 Design Goals

- 🪟 **Native Windows UI** — WinUI 3, not Electron
- 🎨 **Calm, premium, data-dense** presentation
- ⚡ **Fast real-time updates** without polling work on the UI thread
- ✅ **Honest metric availability** — no fabricated values
- 🌍 **Russian & English** localization
- 📦 **Packaged for local distribution** and evaluation

<br>

## 💻 Supported Platforms

| OS | Version | Architecture |
|---|---|---|
| Windows 10 | 22H2 | x64 |
| Windows 11 | 22H2+ | x64 |

<br>

## 📋 Runtime Requirements

The packaged desktop build is **framework-dependent**. The target machine may require:

- [.NET 8 Desktop Runtime](https://dotnet.microsoft.com/en-us/download/dotnet/8.0)
- [Windows App SDK Runtime](https://learn.microsoft.com/en-us/windows/apps/windows-app-sdk/downloads) compatible with the build

<br>

## 🚀 Getting Started

### Running from source

```powershell
# Build
dotnet build .\src\Zxc.Aida.App.UI\Zxc.Aida.App.UI.csproj `
    -c Debug -r win-x64 -m:1 `
    -p:BuildInParallel=false `
    -p:RestoreIgnoreFailedSources=true

# Run
dotnet run --project .\src\Zxc.Aida.App.UI\Zxc.Aida.App.UI.csproj `
    -c Debug -r win-x64 --no-build
```

### Creating a Release build

```powershell
dotnet publish .\src\Zxc.Aida.App.UI\Zxc.Aida.App.UI.csproj `
    -c Release -r win-x64 -m:1 `
    -p:BuildInParallel=false `
    -p:RestoreIgnoreFailedSources=true `
    -p:WindowsPackageType=None `
    -p:WindowsAppSDKSelfContained=false `
    --self-contained false
```

<br>

## 📦 Delivery Package

The repository includes a delivery script that creates a structured release folder:

| Output | Description |
|---|---|
| `source/` | Source snapshot folder and `.zip` archive |
| `github/README.md` | GitHub-ready README copy |
| `README-delivery.md` | Package notes |
| `checksums.txt` | SHA-256 hashes for generated archives |

```powershell
pwsh -File .\build\CreateDelivery.ps1
```

<br>

## 🛠️ Tooling Scripts

| Script | Purpose |
|---|---|
| `build/Build.ps1` | Full project build |
| `build/SmokeTest.ps1` | Quick smoke test |
| `build/PerfTest.ps1` | Performance benchmarking |
| `build/SoakTest.ps1` | Long-running stability test |
| `build/SupportBundle.ps1` | Export support bundle |
| `build/CreateDelivery.ps1` | Create delivery package |

<br>

## 🩺 Support Bundle

The app can export a **support bundle** for troubleshooting, which may include:

- 📄 Settings snapshot
- 🔍 Discovery snapshot
- 📊 Telemetry snapshot
- 📝 Log files
- 🗂️ Manifest metadata

> Intended to simplify support, repro collection, and hardware comparison between systems.

<br>

## 🌡️ Sensor & Telemetry Sources

ZXC.AIDA uses **real Windows and vendor-backed sources** where available:

| Source | Type |
|---|---|
| Windows performance counters & runtime APIs | Built-in |
| Windows ACPI thermal zones | Built-in |
| Windows storage temperature properties | Built-in |
| NVIDIA `nvidia-smi` | Vendor |
| LibreHardwareMonitor / OpenHardwareMonitor WMI | Optional external |

> [!NOTE]
> If a system does not expose a sensor path, the application reports that honestly instead of fabricating a value.

<br>

## 🌍 Localization

| Language | Status |
|---|---|
| 🇷🇺 Russian | ✅ Supported |
| 🇬🇧 English | ✅ Supported |

<br>

## ⚠️ Known Limitations

> [!IMPORTANT]
> - Some temperatures, fan speeds, voltages, and board-level sensors depend on hardware support, drivers, vendor tooling, or optional external monitor namespaces.
> - Full motherboard / EC / Super I/O coverage is **not universally available** through standard Windows user-mode APIs.
> - DIMM temperature is only shown when a real source exposes it.

<br>
