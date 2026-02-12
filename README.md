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
- gdb-multiarch
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

`cwd = bms`  

1. mkdir build && cd build 
2. cmake .. 
3. cmake --build build
## How to Contribute: 

Development of new features will be done on a separate branch other than main and will be merged with a pull request


## ARM Cortex Debug Configuration 
ARM Cortex Debug is a handy VS Code extension that integrates a IDE-like debugger for ARM microcontrollers into VS Code. To set up the debugger follow the instructions below.

1. Type the following command in the top bar: `>Debug: Add Configuration` to generate a 
`launch.json` file in the `.vscode` directory (usually hidden by default). 

2. Navigate and open up the `.vscode/launch.json` file.

3. Copy and paste the following JSON formatted code into the `launch.json` file. This will enable the use of openocd and gdb-mulitarch
by the Cortex Debug extension.

```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug (OpenOCD)",
            "cwd": "${workspaceFolder}",
            "executable": "${workspaceFolder}/bms/build/bms.elf",
            "request": "launch",
            "type": "cortex-debug",
            "servertype": "openocd",
            "interface": "swd",
            "device": "STM32H7532ZI",
            "runToEntryPoint": "main",
            "showDevDebugOutput": "raw",
            "configFiles": [
                "/usr/share/openocd/scripts/interface/stlink.cfg",
                "/usr/share/openocd/scripts/target/stm32h7x.cfg"
            ],
            "preLaunchCommands": [
                "set mem inaccessible-by-default off",
                "monitor reset"
            ],
            "postLaunchCommands": [
                "monitor reset init",
                "monitor sleep 200"
            ],
            "armToolchainPath": "/usr/bin/",
            "gdbPath": "/usr/bin/gdb-multiarch"
        }
    ]
}
```


4. Next, build and compile the binary executable for the project if you haven't already. 


5. Now, press the `Run` option on the top toolbar and select the first option `Start Debugging`
to start a session of Cortex debug. Cortex debug should flash the program to the MCU and highlight the starting point of the program in yellow. On the top right, a toolbar should appear with a few commands for debugging the program.


