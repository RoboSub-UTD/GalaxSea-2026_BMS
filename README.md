# GalaxSea 2026 Battery Management System

The battery management system for GalaxSea 2026 Roboboat

## Documentation
[Add link to documentation folder here]

## Getting started 
Clone the project with `git clone https://github.com/RoboSub-UTD/GalaxSea-2026_BMS.git` 


## Prerequsities 
Ensure the following tools are installed: 
- make 
- CMake
- gcc-arm-none-eabi
- openocd 
- CubeMX (Standalone or included with STM32CubeIDE)

> [!NOTE] 
> installation of some of these tools on a Windows environment may require use of toolchains such as MinGW or Cygwin 

## Recommended VS Code extensions
```
twxs.cmake
marus25.cortex-debug
ms-vscode.vscode-serial-monitor
ms-vscode.makefile-tools
ms-vscode.cmake-tools
ms-vscode.cpptools
ms-vscode.cpptools-extension-pack
ms-vscode.cpptools-themes
mcu-debug.rtos-views
mcu-debug.debug-tracker-vscode
mcu-debug.memory-view
mcu-debug.peripheral-viewer
```

## How to run Firmware

1. mkdir build 
2. cmake --preset Debug
## How to Contribute: 

Development of new features will be done on a separate branch other than main and will be merged with a pull request

