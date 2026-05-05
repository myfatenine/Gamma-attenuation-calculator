# Gamma Attenuation Calculator

Gamma Attenuation Calculator is a Qt Widgets application for calculating gamma-ray attenuation coefficients and shielding thicknesses for different materials.

The project was migrated from the original C# WinForms version to a C++/Qt implementation on April 30, 2026. The Qt version keeps the original single-element attenuation workflow and input validation, adds Chinese/English UI support, and extends the calculator with mixture attenuation by molecular formula parsing or manually entered element mass percentages.

## Features

- Single-element gamma-ray attenuation calculation.
- Mixture calculation from molecular formulas, such as `H2O`, `CaCO3`, and `Fe2(SO4)3`.
- Manual mixture calculation by element symbol or atomic number and mass percentage.
- Chinese and English interface switching.
- Attenuation curve drawing up to 99% attenuation.
- Half-value layer and 95% attenuation thickness markers.
- CSV export for calculated attenuation curves.
- Windows desktop build and Android arm64-v8a APK build support.

## Reference

This program refers to the method and data treatment described in:

https://doi.org/10.1140/epjd/e2017-70679-7

If this project infringes your rights or interests, please contact the maintainer for removal or correction.

## Requirements

### Windows

- Qt 6.11.0 or compatible Qt Widgets kit.
- CMake 3.16 or newer.
- A supported C++17 compiler.

### Android

- Qt 6.11.0 Android `arm64-v8a` kit.
- Android SDK platform 36.
- Android NDK r27c, for example `27.2.12479018`.
- JDK 17.
- Ninja.

The current tested local paths are:

```text
Qt:          E:/Qt/6.11.0/android_arm64_v8a
Android SDK: E:/Android/Sdk
Android NDK: E:/Android/Sdk/ndk/27.2.12479018
Ninja:       E:/Qt/Tools/Ninja/ninja.exe
```

## Build

### Windows Desktop

From the source directory:

```powershell
cmake -S . -B build -DCMAKE_PREFIX_PATH=E:/Qt/6.11.0/mingw_64
cmake --build build --config Release
```

Adjust `CMAKE_PREFIX_PATH` to match your local Qt desktop kit.

### Android APK

The repository includes a helper script:

```powershell
.\build_android_arm64.ps1
```

The APK will be generated under the Android build directory, for example:

```text
build-android-arm64/android-build/build/outputs/apk/debug/android-build-debug.apk
```

On Windows, if Qt Android automoc or Ninja stalls in a long path or a path containing spaces, build through a short path without spaces. For example, create a junction such as `E:/gacsrc` pointing to the source directory and use `E:/gacb` as the build directory.

## Data File

`data.csv` contains the fitted attenuation coefficient parameters used by the calculator. Desktop builds copy this file next to the executable. Android builds embed it through `resources.qrc`, so the APK does not need an external data file.

## Source Layout

```text
CMakeLists.txt
main.cpp
MainWindow.h / MainWindow.cpp
AttenuationCalculator.h / AttenuationCalculator.cpp
AttenuationPlot.h / AttenuationPlot.cpp
data.csv
resources.qrc
android/
build_android_arm64.ps1
```

## License And Disclaimer

This project is provided for research, education, and engineering reference. Calculation results should be independently verified before use in safety-critical shielding design, radiation protection, medical, industrial, or regulatory work.

If any referenced data, method, text, or asset infringes your rights and interests, please contact the maintainer to request deletion or correction.
