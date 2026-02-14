# GalaxSea 2026 Battery Management System

The battery management system for GalaxSea 2026 Roboboat

## Documentation
[Add link to documentation folder here]

## Getting started 
Clone the project with `git clone https://github.com/RoboSub-UTD/GalaxSea-2026_BMS.git` 


## Prerequsities 
Ensure the following tools are installed: 
- make 
- cmake
- gcc-arm-none-eabi
- openocd 
- gdb-multiarch
- CubeMX (Standalone or included with STM32CubeIDE)

> [!NOTE] 
> Installation of some of these tools on a Windows environment may require use of toolchains such as MYSY2 or Cygwin. Installing Windows Subsystem for Linux (WSL2) or using a Linux virtual machine are both viable alternatives.
 

### Installing USB Passthrough (WSL2)
Read this section if you are setting up your build environment through WSL2. You may skip this section otherwise.

USB passthrough is required for WSL2 because WSL2 is essentially a lightweight VM that does not have access to external USB devices by default. We can allow WSL to access USB devices through the use of usbipd-win which can be installed via the following link. The link also includes instructions on how to bind usb devices to WSL2.

usbipd-win Installation Link: https://github.com/dorssel/usbipd-win

> [!TIP]
> Binding devices using usbipd-win requires using the command line. If you prefer to use a GUI then it's reccomended to install 
> `wsl-usb-manager` here 
> https://github.com/nickbeth/wsl-usb-manager



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


