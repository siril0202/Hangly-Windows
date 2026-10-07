# Hangly for Windows

**A charm hangs from a rope on your desktop.** Push it and it swings, with the weight and
the settle of a real one. That is the whole app.

[![Build](https://github.com/siril0202/Hangly-Windows/actions/workflows/build.yml/badge.svg)](https://github.com/siril0202/Hangly-Windows/actions/workflows/build.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

<img src="Docs/media/charm-on-desktop.png" alt="Three charms hanging on a gold chain over a Windows desktop" width="380">

A port of [Hangly for macOS](https://portfolio.codewithsiril.site), written
in C# on WinUI 3, .NET 9 and Win2D. Windows 10 and 11, x64 and ARM64. Brought to Windows by [CodeWithSiril Technologies](https://codewithsiril.site).

> **Hangly for Windows is in public beta.** It works, it is tested, and it is not signed
> yet — so Windows will warn you the first time you run it. [What to
> expect](TESTER-INSTRUCTIONS.md).

---

## What it does

- **Seventy charms**, in collections — protection, luck, ritual, and a few from stories
  you will recognise. Search them, favourite them, see what you hung recently.
- **Up to three on one cord**, each at its own size, in any order you drag them into.
- **Nine rope styles.** Each one is a different set of solver values rather than a
  different picture, so a gold chain hangs differently from a thread.
- **Real physics.** Twenty segments solved with Verlet integration at a fixed 240 Hz,
  whatever the display is doing. Beads ride the cord as particles in their own right.
- **Make your own.** Drop a PNG, a JPG or an SVG on the charm, or use the **Create** tab,
  and it becomes a charm that hangs like the rest.
- **It stays out of the way.** Click-through everywhere except the charm itself, quiet at
  idle — about 1% of one core — and it asks for no permissions at all.

<img src="Docs/media/library.png" alt="The Hangly Library, showing a charm's detail panel, the charms on the cord, and the collections" width="820">

## Technology Stack
- **Framework:** .NET 9.0
- **UI Framework:** WinUI 3 (Windows App SDK)
- **Graphics:** Win2D, SkiaSharp
- **Updater:** Velopack
- **AI/ML:** ONNX Runtime DirectML (for offline subject cutouts)

## Requirements

To build and run the project in Visual Studio, you need:
- **Visual Studio 2022** (v17.12 or newer for .NET 9 support)
- **Workloads:**
  - .NET desktop development
  - Windows application development
- **.NET SDK:** .NET 9.0 SDK
- **Windows SDK:** 10.0.22621.0 or newer
- **OS:** Windows 10 (1809 or later) or Windows 11

### Visual Studio Setup

1. Clone the repository:
   ```cmd
   git clone https://github.com/siril0202/Hangly-Windows.git
   cd Hangly-Windows
   ```
2. Open `Hangly.sln` in Visual Studio 2022.
3. Wait for NuGet packages to restore automatically.
4. Set **Hangly.App** as the Startup Project (Right-click `Hangly.App` -> Set as Startup Project).
5. Select the `Debug` configuration and your target platform (`x64` or `ARM64`, depending on your machine). *Note: `Any CPU` is not supported for the App project due to WinUI 3 requirements.*
6. Press `F5` to build and debug.

### Command Line Build

```powershell
# The solver and models (runs anywhere)
dotnet test tests/Hangly.Core.Tests/Hangly.Core.Tests.csproj

# The app (Windows only)
dotnet run --project src/Hangly.App/Hangly.App.csproj -c Release -r win-x64 -p:Platform=x64
```
For ARM64, use `-r win-arm64 -p:Platform=ARM64`.

## Publishing and Installer

To build an installer, the project uses Velopack. The `EnableMsixTooling` property in `Hangly.App.csproj` must stay enabled for proper XAML compilation.
You can create a release build with Velopack's CLI (`vpk`), exactly as seen in `.github/workflows/release.yml`.

## Configuration

This project does not use `.env` files. Instead, it relies on:
- **`Directory.Build.props` / `Hangly.App.csproj`**: Contains build-time configurations such as branding, assembly metadata, and GA4 Analytics configuration (passed via MSBuild parameters like `-p:HanglyGa4MeasurementId`).
- **`AppSettings.cs`**: Runtime configuration is serialized to a local JSON file (typically located in `%APPDATA%\Hangly`). This contains user preferences like `DisplayName`, `OverlaySettings`, and `PrivacySettings`. There are no sensitive connection strings or API keys stored here.

There is no external database or backend service required.

## Links

- **Website:** [https://codewithsiril.site](https://codewithsiril.site/)
- **Portfolio:** [https://portfolio.codewithsiril.site](https://portfolio.codewithsiril.site/)
- **GitHub:** [https://github.com/siril0202](https://github.com/siril0202)
- **LinkedIn:** [https://linkedin.com/in/santhana-siril](https://linkedin.com/in/santhana-siril)
- **Instagram:** [https://instagram.com/codewithsiril](https://instagram.com/codewithsiril)
- **Business Email:** [codewithsiril.dev@gmail.com](mailto:codewithsiril.dev@gmail.com)

## License and Attribution

- The source code is licensed under the [MIT License](LICENSE).
- **Original Author Attribution:** Copyright (c) 2026 sharancreatedthis.
- **CodeWithSiril Technologies:** Modifications and Windows branding are Copyright © 2026 CodeWithSiril Technologies. All rights reserved.
- The charm artwork and original design assets are subject to the restrictions in [NOTICE.md](NOTICE.md).
