---
layout: research
researchcategory: Savefile
structure: urbzgba
title: Save Info
description: Save Information for The Urbz - Sims in the City Game Boy Advance.
permalink: /research/urbzgba/savefile
---

## Basic Save Structure

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


## Detecting the Savefile
1. Check that the Savefile's size is `0x10000` in size.
2. Check the first `0x8 bytes` that they contain: `0x55 0x52 0x42 0x5A 0x30 0x30 0x31 0x31 (URBZ0011)`.

If all the things pass, congrats you just detected a `The Urbz - Sims in the City (GBA)` Savefile!
<hr>