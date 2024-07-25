---
title: Installation
type: docs
weight: 10
---

# Installation

1. Install the `C/C++ extension for VS Code` extension in Visual Studio Code
2. Download the latest [MSYS2 installer](https://www.msys2.org/)
3. Open a MSYS2 terminal window and install the MinGW-w64 toolchain
   ```sh
   pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
   ```
   > Accept the default number of packages in the `toolchain` group by pressing `Enter`.
4. Add the path of your MinGW-w64 bin folder to the Windows PATH environment
   > If you used the default settings above, then this will be the path: `C:\msys64\ucrt64\bin`.
5. Check your MinGW installation
   ```sh
   gcc --version
   g++ --version
   gdb --version
   ```
