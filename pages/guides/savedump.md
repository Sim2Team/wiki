---
layout: sidebar
sidebar: guides
content-text: Other Guides
title: Save Dump
description: How to dump the Savefile.
permalink: /guides/savedump
---

## How to dump a Game Boy Advance Savefile (DS Lite / DS Phat)
<hr>

### 1. What you need
- [GBA Backup Tool](https://gamebrew.org/wiki/GBA_Backup_Tool)
- A program that can extract `.7z` files, the recommended one on Windows is [7-Zip](https://7-zip.org/), on macOS it's [The Unarchiver](https://theunarchiver.com/).
- A Nintendo DS Lite or Nintendo DS Phat.
- A Slot 1 Flashcart.
- Your Game Boy Advance Cartridge of course.

### 2. Preparations
1. Download `GBA Backup Tool` from GameBrew. Then extract the `.7z` file, and then the `.zip` inside it.
2. Place `GBA_Backup_Tool.nds` from the `GBA Backup Tool` directory inside the root of the Flashcart's SD Card.
3. Insert the SD Card back to the Flashcart and start your console.

### 3. Dumping the Savefile
1. Select `GBA Backup Tool` from the File Selector and start it.
2. Insert your Game Boy Advance Cartridge into Slot 2 and press `A` to let it initialize the Game Boy Advance Cart Slot. This may take a few seconds.
3. Press `B` to let it create a new Savefile dump to the Flashcart's SD Card. Then press `A` to confirm the run prompt.

**You can find your Savefile at `fat:/GBA_Backup/` on your Flashcart's SD Card.**

### 4. Restoring a Savefile
1. Follow Step 1 and 2 from `3. Dumping the Savefile`.
2. Press `R` to let it switch into the `Save Restore` mode. (You can see in which mode it is, by looking at the second blue box on the bottom screen).
3. Select the Savefile from the list on the top screen you want to restore, then press `A`. Read the prompt and press `A` again to confirm it.


<hr>
## How to dump a Nintendo DS Savefile (3DS)
<hr>

### 1. What you need
- [Checkpoint's latest release](https://github.com/FlagBrew/Checkpoint/releases). You should already have that if you followed the [3ds.hacks.guide](https://3ds.hacks.guide/).
- Your Nintendo DS Cartridge of course.
- [Custom Firmware (CFW)](https://3ds.hacks.guide/) installed.

### 2. Preparations
1. Download `Checkpoint` from GitHub.
- Note: Download the `3dsx` file and place it inside the `3ds` directory, if you want to use Checkpoint from the Homebrew Launcher, or the `cia` file and place it anywhere you want, if you want to use Checkpoint from the HOME Menu.

2. If you are using the cia version, just install it like you are used to with [FBI](https://github.com/Steveice10/FBI/releases).
3. Insert your DS Game Cartridge into the Game Slot and make sure it gets detected properly.

### 3. Dumping the Savefile
1. Open Checkpoint (For the `cia` version just start the Flag icon app, for the `3dsx` version just open the Homebrew Launcher and start Checkpoint), then wait until it finished loading.
2. Select your DS Game (which should always be the first icon in the list), then press `A`.
3. Press on `Backup` and confirm with `A`. Then give your Savefile a name. You could just call it `Dump` for a test.
4. Wait until it finishes by displaying `Progress correctly saved to disk.`.

**You can find your Savefile at `sdmc:/3ds/Checkpoint/saves/<Game>/<Name of the Backup>/`.**

### 4. Restoring a Savefile
1. Follow Step 1 and 2 from `3. Dumping the Savefile`.
2. Select the Dump from the list you want to restore, then press on `Restore` and confirm the prompt with `A`.
3. Wait until it finishes by displaying `<Dump Name> has been restored successfully.`.

**There are also some things you have to keep in mind when using Checkpoint, for more see below.**

### 5. Additional Notes
- **Checkpoint stores the Nintendo DS Savefiles as the following after the `saves` directory:**
    - `ASI(E / J / P) THE URBZ DS` for The Urbz - Sims in the City.
    - `ASJ(E / J / P) THE SIMS 2` for The Sims 2.
	- **The last letter after the first 3 characters depends on the region of your Cartridge. `E` being English (which is USA/North America), `J` being Japanese and `P` being PAL.**

- **For a proper Savefile restore, the Savefile MUST exactly be called like this for the games:**
    - `The Urbz - Sims in the City` -> `THE URBZ DS.sav`.
    - `The Sims 2` -> `THE SIMS 2.sav`.
	

<hr>
## How to dump a Nintendo DS Savefile (DSi)
<hr>

### 1. What you need
- [GodMode9i's latest release](https://github.com/DS-Homebrew/GodMode9i/releases).
- A program that can extract `.7z` files, the recommended one on Windows is [7-Zip](https://7-zip.org/), on macOS it's [The Unarchiver](https://theunarchiver.com/).
- Your Nintendo DS Cartridge of course.
- [Unlaunch](https://dsi.cfw.guide/) installed for Slot 1 access.

### 2. Preparations
1. Download `GodMode9i.7z` from GitHub.
2. Extract `GodMode9i.nds` from the 7z file.
3. Place `GodMode9i.nds` from the `GodMode9i` directory inside the root of the DSi SD Card.


### 3. Dumping the Savefile
1. Open GodMode9i with Unlaunch, TWiLight Menu++ or whatever you are using to launch Homebrew apps.
2. Insert your Nintendo DS Cartridge into the Slot.
3. Scroll down to `NDS GAMECARD` and then press `X` for `save only`.

**You can find your Savefile at `sd:/gm9i/out/`.**

### 4. Restoring a Savefile
1. Follow Step 1 and 2 from `3. Dumping the Savefile`.
2. Go to `[sd:] "SDCARD"`, then navigate to your Savefile.
3. Select your Savefile, then select `Restore save`.
<hr>