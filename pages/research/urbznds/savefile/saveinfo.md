---
layout: research
researchcategory: Savefile
structure: urbznds
title: Save Info
description: Save Information for The Urbz - Sims in the City Nintendo DS.
permalink: /research/urbznds/savefile
---

## Basic Save Structure

| Offset          | Datatype | Size   | Content         |
| --------------- | -------- | ------ | --------------- |
| 0x0 - 0x1F      | uint8_t  | 0x20   | Settings Header |
| 0x20 - 0xFFF    | uint8_t  | 0xFE0  | Slot 1          |
| 0x1000 - 0x1DFF | uint8_t  | 0xFE0  | Slot 2          |
| 0x1EF0 - 0x1FFF | uint8_t  | 0x20   | Unknown         |

<hr>


## Detecting the Savefile
1. Check that the Savefile's size is `0x2000` in size.
2. Check the first `0x8 bytes` that they contain (see below).

- **^ NOTE: Each region has a different header identifier, see below for the proper one.**
    - `0x55 0x52 0x42 0x5A 0x30 0x30 0x31 0x30` => USA.
    - `0x55 0x52 0x42 0x5A 0x30 0x30 0x37 0x30` => Europe.
	- `0x55 0x52 0x42 0x5A 0x4A 0x30 0x30 0x32` => Japan.

If all the things pass, congrats you just detected a `The Urbz - Sims in the City (NDS)` Savefile and also the region!
<hr>