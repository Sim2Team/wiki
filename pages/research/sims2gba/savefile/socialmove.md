---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Social Move
description: The Sims 2 Game Boy Advance | Savefile Social Move Research
permalink: /research/sims2gba/savefile/socialmove
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.0.**
<hr>


## Some notes
- There are 15 Social Moves in game.
- The first Social Move starts at `0x3EE` of the slot.
- The size of the Social Move Structure is: `0x8` (8) bytes.
- The full size for the Social Move section is: `0x78` bytes ( 15 * 0x8 ).

- **NOTE: The final Offset varies with the amount of items you have in your house, see [Social Move Offset](#social-move-offset) for how to get the proper final Offset.**
<hr>


## Structure
You can find a C++ structure for the Social Moves below.

```cpp
struct SocialMove {
	enum class Flag : uint8_t { Locked = 0x0, Unlocked = 0x1, Blocked = 0x2 };

	Flag Status = Flag::Locked; // The Status of the Social Move; 0x0.
	uint8_t Unknown1[0x3] = { 0x0 }; // Unknown; 0x1 - 0x3.
	uint8_t Level = 0x0; // The Level of the Social Move; 0x4.
	uint8_t Unknown2 = 0x0; // Unknown; 0x5.
	uint8_t BlockedHours = 0x0; // The hours for how long it's blocked; 0x6.
	uint8_t Unknown3 = 0x0; // Unknown; 0x7.
};
```
<hr>


## Social Move Offset
The Social Move final offset depends on how many items you have in your House.

The amount of items you have in your house is stored at byte `0xD6` of the SavSlot's Data.

See below for a way how to get the final offset.

```cpp
/*
	SlotData is the data of the SavSlot.
	SocialMoveIdx is the Social Move index ( 0 - 14 ).
*/
uint32_t GetOffset(uint8_t *SlotData, uint8_t SocialMoveIdx) {
	if (SocialMoveIdx >= 15) return 0; // Out of scope. Only 0 - 14 is valid.

	return 0x3EE + (SocialMoveIdx * 0x8) + (SlotData[0xD6] * 0x6);

	/*
		If you instead want to access it directly from the SavData instead of the SlotData, rework it like this:
		Slot being '1' for Slot 1, '2' for Slot 2 etc.

		return (Slot * 0x1000) + 0x3EE + (SocialMoveIdx * 0x8) + (SavData[(Slot * 0x1000) + 0xD6] * 0x6);
	*/
};
```
<hr>


## Social Move List
You can find a list with the base offsets for each Social Move below in the Table.

| Social Move Name     | Start Offset  | End Offset  |
| -------------------- | ------------- | ----------- |
| Chit-Chat            | 0x0           | 0x7         |
| Entertain            | 0x8           | 0xF         |
| Hug                  | 0x10          | 0x17        |
| Brag                 | 0x18          | 0x1F        |
| Apologize            | 0x20          | 0x27        |
| Sweet Talk           | 0x28          | 0x2F        |
| Flirt                | 0x30          | 0x37        |
| Blow Kiss            | 0x38          | 0x3F        |
| Kiss                 | 0x40          | 0x47        |
| Show Off Body        | 0x48          | 0x4F        |
| Annoy                | 0x50          | 0x57        |
| Insult               | 0x58          | 0x5F        |
| Threaten             | 0x60          | 0x67        |
| Rude Gesture         | 0x68          | 0x6F        |
| Karate Moves         | 0x70          | 0x77        |

<hr>


## Social Move Flags
The flags say, if the Social Move is one of those:

- Locked
- Unlocked
- Blocked

It is stored at byte `0x0` in the structure of the Social Moves.

Below you will find a table with the values and the flags.

| Flag     | Value |
| -------- | ----- |
| Locked   | 0x0   |
| Unlocked | 0x1   |
| Blocked  | 0x2   |

<hr>


## Social Move Levels
The Social Move Level is stored at byte `0x4` in the structure of the Social Moves.

The valid level range is: `0x0` for Level 1 up to `0x2` for Level 3.
<hr>


## Social Move Blocked Hours
The amount of hours the Social Move is blocked is stored at byte `0x6` in the structure of the Social Moves.

If the Social Move gets blocked, it sets that byte to `0xC` which is `12` and means 12 Hours.

Every full hour, that value will decrease for `0x1`.
<hr>