---
layout: research
researchcategory: Savefile
structure: sims2gba
title: House Item
description: The Sims 2 Game Boy Advance | House Item Research
permalink: /research/sims2gba/savefile/houseitem
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.**
<hr>


## Some notes
- There are 12 available Slots for your House.
- The House Items start at `0xD6` of the SavSlot beginning with an House Item Count.
- The size of an House Item is `0x6` bytes.
- The full size for the House Items section is: `0x49` bytes ( 0x1 + ( 12 * 0x6 ) ).

### Other technical notes
- If you add one item, then the item is getting inserted at Offset `0xD7` of the SavSlot. This is, what causes things to move up for `0x6` starting at `0xD7` at the SavSlot.
- If you remove an item, then the 0x6 bytes, which is the size of an House Item gets removed and things move down for `0x6`.

**TODO for both: Figure out, how many bytes exactly move, as the Checksum always stays at the same location at `0xFFE - 0xFFF`.**
<hr>


## Structure
You can find a C++ structure for the House Items below.

```cpp
struct Item {
	enum class ItemDirection : uint8_t { Right = 0x1, Down = 0x3, Left = 0x5, Up = 0x7 }; // Item Directions.

	uint8_t ID = 0xE6; // The Item ID; 0x0.
	uint8_t Flag = 0x0; // The Item Flag; 0x1.
	uint8_t UseCount = 0x0; // The Item Use Count; 0x2.
	uint8_t XPosition = 0x0; // The X-Position of the Item; 0x3.
	uint8_t YPosition = 0x0; // The Y-Position of the Item; 0x4.
	ItemDirection Direction = ItemDirection::Down; // The Item Direction; 0x5.
};


struct HouseItems {
	uint8_t Count = 0x0; // The amount of Items from the House; 0x0.
	Item Slot1; // The first House Item; 0x1 - 0x6.
	Item Slot2; // The second House Item; 0x7 - 0xC.
	Item Slot3; // The third House Item; 0xD - 0x12.
	Item Slot4; // The fourth House Item; 0x13 - 0x18.
	Item Slot5; // The fifth House Item; 0x19 - 0x1E.
	Item Slot6; // The sixth House Item; 0x1F - 0x24.
	Item Slot7; // The seventh House Item; 0x25 - 0x2A.
	Item Slot8; // The eighth House Item; 0x2B - 0x30.
	Item Slot9; // The nineth House Item; 0x31 - 0x36.
	Item Slot10; // The tenth House Item; 0x37 - 0x3C.
	Item Slot11; // The eleventh House Item; 0x3D - 0x42.
	Item Slot12; // The twelveth House Item; 0x43 - 0x48.
};
```
<hr>


## Item IDs
For a list of all Item IDs, checkout the [Item ID Section](item#item-id-list).
<hr>


## Item Flags
For a list of all Item flags, checkout the [Item Flags Section](item#item-flags).

**NOTE, that this section is a TODO.**
<hr>


## Item Use Count
For a list of all Item Use Counts, checkout the [Item Use Count Section](item#item-use-count).

**NOTE, that this section is a TODO.**
<hr>


## Item X-Position
**TODO: Figure out what's the max X-Position for the House Items.**
<hr>


## Item Y-Position
**TODO: Figure out what's the max Y-Position for the House Items.**
<hr>


## Item Direction
The last byte of the House Items store a direction. Below you will find a table with the Directions and the Values.

| Direction | Value |
| --------- | ----- |
| Right     | 0x1   |
| Down      | 0x3   |
| Left      | 0x5   |
| Up        | 0x7   |

It might be possible that they repeat at larger values, i haven't looked into it yet.
<hr>