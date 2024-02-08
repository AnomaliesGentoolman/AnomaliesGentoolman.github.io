---
layout: post
title: Compiled Terraria And TModloader Source Code with Goldberg
description: Compiled Terraria and Tmodloader with Goldberg Steam Emulator
tags: terraria tmodloader goldberg
---

# Amnesia: The Dark Descent with Fixed Tools!

This is a fork of the Amnesia the Dark Descent repository from FrictionalGames.

# Fixed Tools and Other

The Trick That I Did
---
I copied Amnesia: A Machine For Pigs tools and pasted into **"HPL2"** (Engine) Folder and they actually worked well.

About Visual Studio C++ 2010
---
If you cant find the Visual Studio C++ 2010 Express, then you can download from here: https://mega.nz/file/334wXAoR#5TAzdDb0Y81wzSubV7ri3yK_ni5IzCT-LYOx5wg0D50

You need to install C++ version of 2010, just mount the iso and go over to **VCExpress** and open **setup.exe**

I just get that file from **my.visualstudio.com** that is by Microsoft, You need **Dev Essentials** for access older versions of Visual Studio but i did it for you guys already and published in **MEGA**.

## Index

* [Windows](#project-overview-windows) - Compiling instructions for Windows.
* [Linux](#building--playing-linux) - Compiling instructions for Linux.

## Prerequisites
All releases:
- A copy of Amnesia: the Dark Descent (For playing the game, many files necessary for launching don't come with the source code)

Windows:
- Visual Studio C++ 2010 Express: **[You can find the link on top.](#about-visual-studio-c-2010)**
- .NET Desktop Development: You can install this in Visual Studio Installer, If you have 2019 or 2022 version just modify it.
- VS 2010 Service Pack 1: https://www.microsoft.com/en-us/download/details.aspx?id=34677 or get from the repository.
- You can also use a newer VS version for compiling as long as you have the 2010 one too

Linux:
- CMake, Make (for compiling)

## Project Overview (Windows)
The game is built from two separate solutions: The engine solution named `HPL2_2010` and the main game solution named `Lux`.
The project also includes all the different editors and additional tools, such as the Level Editor and the Model Editor.

### Engine Overview
Todo: Add some descriptions about what kind of files we have in the engine solution.

### Game Overview
Todo: Add some descriptions about what kind of files we have in the game solution.

## Building & Playing (Windows)
In order to build the game on Windows, you will first need to compile and build the HPL2 Engine.

### Building the Engine
1. Clone the project
2. Go to the `HPL2/` folder and extract `dependencies.zip`.
3. Open `_HPL2_2010.sln` with Visual Studio 2010.
4. Set the build configuration from `Debug` to `Release`.
5. `Build -> Build _HPL2_2010`. There won't be any errors, but some warning messages will appear.
6. The build result will be created in `HPL2/lib`

### Building the Game
1. Go to `amnesia/src/game` and open `Lux.sln`.
2. Click cancel on retag project message.
3. Set the build configuration from `Debug` to `Release`.
4. `Build -> Build Lux`.  There won't be any errors, but some warning messages will appear.
5. The game executable should be created in `amnesia/redist`.

### Playing the Game
Copy `Amnesia.exe` into your Amnesia game folder and launch it. The main menu should appear normally with no errors.

## Building & Playing (Linux)

There are a few extra steps required to be able to successfully build everything on Linux compared to Windows.

### Building the Engine, Game & Editors

1. Ensure you have `make` and `cmake` installed.
2. Clone the project and enter the folder
3. Extract `./HPL2/dependencies.zip` to the same folder it's in
4. Run the script file at `./HPL2/dependencies/lib/linux/lib64/fix_symlinks.sh` to fix broken symlinks from the .zip file
5. Open a terminal in `./amnesia/src` and run `cmake .`
6. With a terminal in `./amnesia/src` do `make` (or use `make -jX` where X is the number of jobs you want to run to speed things up, based on your CPU threads)
7. The build should compile and the resulting binaries will be found in `./amnesia/src`

### Playing the Game

To run the compiled binary, copy it to your Amnesia installation folder. For example copy the `Amnesia.bin.x86_64` to your game folder. Run it, and the game should start directly.

## Troubleshooting
* **"When I compile `Lux`, I get an error message "fatal error RC1015: cannot open include file 'afxres.h'".**"
* You need to install the `Microsoft Foundation Classes for C++`. If it still doesn't work, change `afxres.h` to `windows.h`. It should compile then.

* **"When I compile the level editor, I get error message about vc70 not found.**"
* Try turning the Pre-Link Event off. Go to `Project Properties -> Build Events -> Pre-Link Event`, set `Use In Build` to `No` and build again.
