# Munchies

C++17 + SDL3. SDL3 is fetched and built automatically by CMake (pinned to
`release-3.4.20`), so there is nothing to install besides a compiler and CMake.

## Prerequisites
- CMake >= 3.24, git, a C++17 compiler
- macOS: `xcode-select --install`
- Linux (Debian/Ubuntu): `sudo apt install build-essential cmake git libx11-dev libxext-dev libwayland-dev libxkbcommon-dev libasound2-dev libpulse-dev libgl-dev libdrm-dev libgbm-dev`
- Windows: Visual Studio 2022 (C++ workload)

## Build & run
```bash
cmake -S . -B build
cmake --build build -j
./build/Munchies        # Windows: build\Debug\Munchies.exe
```
The first configure downloads SDL3 (needs internet); later ones are cached in `build/`.

## Changing the SDL version
Edit `GIT_TAG` in `CMakeLists.txt` and commit it so everyone stays in sync.
Use an already-installed SDL3 instead with `-DMUNCHIES_USE_SYSTEM_SDL3=ON`.
