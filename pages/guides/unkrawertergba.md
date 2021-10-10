---
layout: sidebar
sidebar: guides
content-text: Other Guides
title: Unkrawerter GBA
description: How to export the Game Boy Advance Soundtracks to the best quality as a WAV, MP3 whatever you like
permalink: /guides/unkrawertergba
---

### 1. What you need
- [UnkrawerterGBA](https://github.com/MCJack123/UnkrawerterGBA/releases)
- [OpenMPT](https://openmpt.org/)
- A dump of your `The Sims Bustin' Out`, `The Urbz - Sims in the City` or `The Sims 2` Game Boy Advance.

### 2. Extracting S3M Modules out of the ROM
1. Download UnkrawerterGBA's latest release.
2. Open a command prompt where you placed `UnkrawerterGBA` and type `.\UnkrawerterGBA.exe <Path to your GBA ROM Dump of Bustin' Out, The Urbz or Sims 2>`. This command may vary per OS, Windows 10 is used in this example.

***Note: Don't type the `<>`'s on that command, only type the Path to the ROM.***

**It should now have extracted `S3M` files inside the directory where you have the command prompt open. It may also extract `XM` files, but that should also work.**

### 3. Converting the Modules to whatever file format you want
1. Download OpenMPT and install it. Then run it.
2. Go to `File` -> `Open...` and select your extracted `S3M` file.
3. Select the opened file on the sidebar. Then you can also listen to it first.
4. Go to `File` -> `Stream Export (WAV, FLAC, MP3, etc)...`.
5. Select in which format you want to convert it as at `Format`.
6. Press on `OK` and select where you want to export the file. You can also edit the Metadata and such before and some other things.

**Congrats, you just got the soundtrack in whatever format you want.. directly extracted of your ROM Dump!**

### 4. Additional Notes
- UnkrawerterGBA only works with games that use the Krawall sound engine, all The Sims Game Boy Advance Spin-Off games use this.
- You can also put UnkrawerterGBA to your PATH and type the command like this: `UnkrawerterGBA <Path/To/Your/ROM.gba>`. It will export the `S3M` files then where you have the command prompt open when running the command.
- You may want to increase the `Sample Volume` first to the max, to get the best sound volume out of it.