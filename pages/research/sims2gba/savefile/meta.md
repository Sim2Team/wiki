---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Meta
description: The Sims 2 Game Boy Advance | Meta Research
permalink: /research/sims2gba/savefile/meta
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.**
<hr>


## Some notes
The only things I know so far are:

- It doesn't seem to have a Checksum in place.
- It seems to be related to the last played slot data. This is completely unresearched as I haven't gotten into yet.
- The section seems to start at `0x19` up to `0xFFF` or something like that.
- I'm not even sure what that section is... so I just call it "Meta" for now, lol.
<hr>


## Structure
You can find a C++ structure for the Meta below.

```cpp
struct Meta {
	uint8_t Unknown[0xFE7] = { 0x0 }; // Just completely unresearched yet; 0x0 - 0xFE6.
};
```
<hr>