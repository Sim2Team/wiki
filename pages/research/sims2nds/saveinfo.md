---
layout: research
researchcategory: Savefile
structure: sims2nds
title: Save Info
description: Save Information for The Sims 2 Nintendo DS.
permalink: /research/sims2nds
---

## Basic Save Information

| Content  | Answer                                               |
| -------- | ---------------------------------------------------- |
| Savesize | 256 KB (0x40000)                                     |
| Savetype | TODO                                                 |
| Gamecode | ASJP (PAL), ASJE (USA/NA), ASJP (JPN)                |

<hr>


## Basic Save Structure

| Offset           | Datatype | Size    | Content         |
| ---------------- | -------- | ------- | --------------- |
| 0x0 - 0xFFF      | uint8_t  | 0x1000  | Slot 1          |
| 0x1000 - 0x1FFF  | uint8_t  | 0x1000  | Slot 2          |
| 0x2000 - 0x2FFF  | uint8_t  | 0x1000  | Slot 3          |
| 0x3000 - 0x3FFF  | uint8_t  | 0x1000  | Slot 4          |
| 0x4000 - 0x4FFF  | uint8_t  | 0x1000  | Slot 5          |
| 0x5000 - 0x9FFF  | uint8_t  | 0x5000  | Paintings       |
| 0xA000 - 0x3FFFF | uint8_t  | 0x36000 | Unknown         |

<hr>


## Detecting the Savefile
1. Check that the Savefile's size is `0x40000` in size.
2. Check the first `0x8 bytes` on the following locations:
    - 0x0
	- 0x1000
	- 0x2000
	- 0x3000
	- 0x4000

And make sure that at least one of the locations contain (see below).

- **^ NOTE: Each region has a header identifier, see below for the proper one.**
    - `0x64 0x61 0x74 0x00 0x1F 0x00 0x00 0x00` -> USA / NA.
    - `0x64 0x61 0x74 0x00 0x20 0x00 0x00 0x00` -> PAL.
	- `0x64 0x61 0x74 0x00 0x21 0x00 0x00 0x00` -> JPN.

If all the things pass, congrats you just detected a `The Sims 2 (NDS)` Savefile and also the region!
<hr>