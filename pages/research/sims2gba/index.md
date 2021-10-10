---
layout: research
structure: sims2gba
title: Index
description: Index page for The Sims 2 (GBA) research.
permalink: /research/sims2gba
---

### Save Informations

**Basic Save Structure**

| Offset          | Datatype | Size   | Content         |
| --------------- | -------- | ------ | --------------- |
| 0x0 - 0x18      | uint8_t  | 0x19   | Settings Header |
| 0x19 - 0xFFF    | uint8_t  | 0xFE7  | Meta Data       |
| 0x1000 - 0x1FFF | uint8_t  | 0x1000 | Slot 1          |
| 0x2000 - 0x2FFF | uint8_t  | 0x1000 | Slot 2          |
| 0x3000 - 0x3FFF | uint8_t  | 0x1000 | Slot 3          |
| 0x4000 - 0x4FFF | uint8_t  | 0x1000 | Slot 4          |
| 0x5000 - 0xFFFF | uint8_t  | 0xB000 | Unused          |

<hr>

**Basic Save Information**

| Content  | Answer                                               |
| -------- | ---------------------------------------------------- |
| Savesize | 64 KB (0x10000)                                      |
| Savetype | FLASH 512k                                           |
| Gamecode | B46P (PAL), B46E (USA/NA)                            |

<hr>


**Detecting the Savefile**
1. Check that the Savefile's size is `0x10000` in size.
2. Check the first `0x7 bytes` that they contain: `0x53 0x54 0x57 0x4E 0x30 0x32 0x34`.

If all the things pass, congrats you just detected a `The Sims 2 (GBA)` Savefile!