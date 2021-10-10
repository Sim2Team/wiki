---
layout: research
structure: bustinout
title: Index
description: Index page for The Sims Bustin' Out (GBA) research.
permalink: /research/bustinout
---

### Save Informations

- The Japanese version has a completely different Gamecode compared to the PAL version.
- The USA / NA version has 2 revisions, according to Retroarch's Database Info the Gamecode is `ASIE`.


**Basic Save Structure**

| Offset          | Datatype | Size  | Content         |
| --------------- | -------- | ----- | --------------- |
| 0x0 - 0xF       | uint8_t  | 0x10  | Settings Header |
| 0x10 - 0x807    | uint8_t  | 0x7F8 | Slot 1          |
| 0x808 - 0xFFF   | uint8_t  | 0x7F8 | Slot 2          |
| 0x1000 - 0x17F7 | uint8_t  | 0x7F8 | Slot 3          |
| 0x1F78 - 0x1FEF | uint8_t  | 0x7F8 | Game Cube Slot  |
| 0x1FF0 - 0x1FFF | uint8_t  | 0x10  | Unknown         |

<hr>

**Basic Save Information**

| Content  | Answer                                               |
| -------- | ---------------------------------------------------- |
| Savesize | 8 KB (0x2000)                                        |
| Savetype | EEPROM 64k                                           |
| Gamecode | ASIP (PAL), ASIE (Not confirmed, USA/NA), B4PJ (JPN) |

<hr>


**Detecting the Savefile**
1. Check that the Savefile's size is `0x2000` in size.
2. Check the first `0x8 bytes` that they contain: `0x30 0x30 0x30 0x30 0x45 0x49 0x53 0x41`.

If all the things pass, congrats you just detected a `The Sims Bustin' Out (GBA)` Savefile!