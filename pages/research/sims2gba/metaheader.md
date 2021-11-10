---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Meta Header
description: The Sims 2 Game Boy Advance | Meta Header Research
permalink: /research/sims2gba/metaheader
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.**
<hr>


## Some notes
- The exact size of the Header is unknown yet. It seems like the Checksum contains the range from `0x0` up to `0x18` though.
- The Checksum of the "Meta Header" is stored at `0xE - 0xF` inside the Savefile.
- The first `0x7` bytes is a identifier for the Savefile, so the game can ensure the Savefile is actually valid. The `ST` could likely mean `Sims, The` from the game title, however `WN024` is unknown yet.
<hr>


## Structure
You can find a C++ structure for the Meta Header below.

```cpp
struct MetaHeader {
	enum class SFXVolumes : uint8_t {
		Vol0 = 0x0, Vol1 = 0xC, Vol2 = 0x18, Vol3 = 0x24, Vol4 = 0x30, Vol5 = 0x3C, Vol6 = 0x48,
		Vol7 = 0x54, Vol8 = 0x60, Vol9 = 0x6C, Vol10 = 0x80
	};

	enum class MUSVolumes : uint8_t {
		Vol0 = 0x0, Vol1 = 0x19, Vol2 = 0x32, Vol3 = 0x4B, Vol4 = 0x64, Vol5 = 0x7D, Vol6 = 0x96,
		Vol7 = 0xAF, Vol8 = 0xC8, Vol9 = 0xE1, Vol10 = 0xFF
	};

	enum class Languages : uint8_t {
		English = 0x0, Dutch = 0x1, French = 0x2, German = 0x3, Italian = 0x4, Spanish = 0x5
	};

	uint8_t Identifier[0x7] = { 0x53, 0x54, 0x57, 0x4E, 0x30, 0x32, 0x34 }; // The identifier the game uses, to validate the Savefile, which is "STWN024"; 0x0 - 0x6.
	uint8_t Unknown1 = 0x0; // Unknown; 0x7.
	SFXVolumes SoundEffectVolume = SFXVolumes::Vol0; // The Sound Effect Volume Level; 0x8.
	MUSVolumes MusicVolume = MUSVolumes::Vol0; // The Music Volume Level; 0x9.
	Languages Language = Languages::English; // The Language the game uses; 0xA.
	uint8_t Unknown2[0x3] = { 0x0 }; // Unknown; 0xB - 0xD.
	uint16_t Checksum = 0x0; // The Meta Header Checksum; 0xE - 0xF.

	uint8_t BigfootLovesChickens : 4; // Bigfoot Loves Chickens Minigame Level; 0x10.
	uint8_t CarCommercials : 4; // Car Commercial Minigame Level; 0x10.
	uint8_t KeelhaulinCards : 4; // Keelhaulin' Cards Minigame Level; 0x11.
	uint8_t CattleCleanup : 4; // Cattle Cleanup Minigame Level; 0x11.
	uint8_t KingChugChug : 4; // King Chug-Chug Minigame Level; 0x12.
	uint8_t CanyonJumping : 4; // Canyon Jumping Minigame Level; 0x12.
	uint8_t ChopShop : 4; // Chop Shop Minigame Level; 0x13.
	
	uint8_t Unknown3 : 4; // Unknown; 0x13.
	uint8_t Unknown4[0x4] = { 0x0 }; // Unknown; 0x14 - 0x18.
};
```
<hr>


## Sound Effect Volumes
The Meta Header at offset `0x8` stores the Sound Effect Volume.

The volumes are not stored like `0x0, 0x1, 0x2` etc, they are directly stored as their percentage or so. See below for the Levels and their actual value.

| Level | Value |
| ----- | ----- |
| 0     | 0x0   |
| 1     | 0xC   |
| 2     | 0x18  |
| 3     | 0x24  |
| 4     | 0x30  |
| 5     | 0x3C  |
| 6     | 0x48  |
| 7     | 0x54  |
| 8     | 0x60  |
| 9     | 0x6C  |
| 10    | 0x80  |

<hr>


## Music Volumes
The Meta Header at offset `0x9` stores the Music Volume.

The volumes are not stored like `0x0, 0x1, 0x2` etc, they are directly stored as their percentage or so. See below for the Levels and their actual value.

| Level | Value |
| ----- | ----- |
| 0     | 0x0   |
| 1     | 0x19  |
| 2     | 0x32  |
| 3     | 0x4B  |
| 4     | 0x64  |
| 5     | 0x7D  |
| 6     | 0x96  |
| 7     | 0xAF  |
| 8     | 0xC8  |
| 9     | 0xE1  |
| 10    | 0xFF  |

<hr>


## Languages
The Meta Header at offset `0xA` stores the active language.

If the language index is `0x6` or larger, the game won't display any text and eventually crash, so be warned. See below for the Language Indexes.

| Language | Index |
| -------- | ----- |
| English  | 0x0   |
| Dutch    | 0x1   |
| French   | 0x2   |
| German   | 0x3   |
| Italian  | 0x4   |
| Spanish  | 0x5   |

<hr>


## Minigames
The Minigames are stored as 4 bits. So 4 bits per minigame starting at `0x10` with `Bigfoot Loves Chickens`.

The range for valid Levels are: `0x0 - 0x5`. Use `0x0` if you don't want the Minigames stored inside the Minigames menu, or `0x1 - 0x5` if you want them there.

See below for a list for which offset and bits is for which Minigame.

| Minigame               | Offset | Bits          |
| ---------------------- | ------ | ------------- |
| Bigfoot Loves Chickens | 0x10   | First 4       |
| Car Commercials        | 0x10   | Last  4       |
| Keelhaulin' Cards      | 0x11   | First 4       |
| Cattle Cleanup         | 0x11   | Last  4       |
| King Chug-Chug         | 0x12   | First 4       |
| Canyon Jumping         | 0x12   | Last  4       |
| Chop Shop              | 0x13   | First 4       |

<hr>