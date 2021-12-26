---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Item Package
description: The Sims 2 Game Boy Advance | Item Package Research
permalink: /research/sims2gba/savefile/itempackage
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.**
<hr>


## Some notes
- There are 6 Item Packages in the Savefile it seems.
- The first Item Package starts at `0x4C` of the slot.
- The size of an Item Package is: `0x13` (19) bytes.
- The full size for the Item Package section is: `0x72` bytes ( 6 * 0x13 ).
- An Item Package contains a item count and 6 Item slots.
<hr>


## Structure
You can find a C++ structure for the Item Packages below.

```cpp
struct Item {
	uint8_t ID = 0xE6; // The Item ID; 0x0.
	uint8_t Flag = 0x0; // The Item Flag; 0x1.
	uint8_t UseCount = 0x0; // The Item Use Count; 0x2.
};


struct ItemPackage {
	uint8_t Count = 0x0; // The amount of active Items from the Package; 0x0.
	Item Slot1; // The first Item Slot from the Package; 0x1 - 0x3.
	Item Slot2; // The second Item Slot from the Package; 0x4 - 0x6.
	Item Slot3; // The third Item Slot from the Package; 0x7 - 0x9.
	Item Slot4; // The fourth Item Slot from the Package; 0xA - 0xC.
	Item Slot5; // The fifth Item Slot from the Package; 0xD - 0xF.
	Item Slot6; // The sixth Item Slot from the Package; 0x10 - 0x12.
};
```
<hr>


## Item IDs
For a list of all Item IDs, checkout the <a href="{{ "/research/sims2gba/item#id-list" | absolute_url }}">Item ID Section</a>.
<hr>


## Item Packages
The game seems to have 6 Item Packages, while only 5 are known yet.

Below you can find a Table of the Item Packages.


| Name           | Start Offset | End Offset |
| -------------- | ------------ | ---------- |
| Pawnshop       | 0x4C         | 0x5E       |
| Saloon         | 0x5F         | 0x71       |
| Skillbook Shop | 0x72         | 0x84       |
| Unknown        | 0x85         | 0x97       |
| Mailbox        | 0x98         | 0xAA       |
| Inventory      | 0xAB         | 0xBD       |

<hr>


## Item Flags
For a list of all Item flags, checkout the <a href="{{ "/research/sims2gba/item#item-flags" | absolute_url }}">Item Flags Section</a>.

**NOTE, that this section is a TODO.**
<hr>


## Item Use Count
For a list of all Item Use Counts, checkout the <a href="{{ "/research/sims2gba/item#item-use-count" | absolute_url }}">Item Use Count Section</a>.

**NOTE, that this section is a TODO.**
<hr>