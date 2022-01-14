---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Episode
description: The Sims 2 Game Boy Advance | Savefile Episode Research
permalink: /research/sims2gba/savefile/episode
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.2.0.**
<hr>


## Some notes
- There are 24 Episodes in game.
- Only 12 of 24 are actually playable, while 11 are only re-play able from the Episode Select Menu.
- The first Episode starts at `0xFF` of the Slot.
- The size of the Episode Structure is: `0x5` (5) bytes.
- The full size for the Episode section is: `0x78` bytes ( 24 * 0x5 ).

- **NOTE: The final Offset varies with the amount of items you have in your house, see [Episode Offset](#episode-offset) for how to get the proper final Offset.**
<hr>


## Structure
You can find a C++ structure for the Episodes below.

```cpp
struct Episode {
	uint8_t PlotPointsCompleted = 0x0; // Plot Points Completed Rating; 0x0.
	uint8_t AspirationConversation = 0x0; // Aspiration Conversation Rating; 0x1.
	uint8_t HiddenWantCompleted = 0x0; // Hidden Want Completed Rating; 0x2.
	uint8_t ErrandCompleted = 0x0; // Errand Completed Rating; 0x3.
	uint8_t Unlocked : 1; // Episode Unlocked State; 0x4 Bit 0.
	uint8_t Played : 1; // Episode Played State; 0x4 Bit 1.
	uint8_t Unknown : 6; // Something to figure out; 0x4 Bit 2 - 7.
};
```
<hr>


## Episode Offset
The Episode final offset depends on how many items you have in your House.

The amount of items you have in your house is stored at byte `0xD6` of the SavSlot's Data.

See below for a way how to get the final offset.

```cpp
/*
	Not necessarily required, but if you just like to use the offsets from the episodes that are displayed on the Episode Selection Screen,
	you can just use that instead of 0xFF.
*/
static constexpr uint32_t EPOffsets[11] = {
	0x104, 0x10E, 0x122, // Season 1.
	0x11D, 0x131, 0x127, 0x14A, // Season 2.
	0x140, 0x118, 0x16D, 0x168 // Season 3.
};

/*
	SlotData is the data of the SavSlot.
	EPIdx is the episode index ( 0 - 23 ).

	For the indexes, check the Episode Table below.
*/
uint32_t GetOffset(uint8_t *SlotData, uint8_t EPIdx) {
	if (EPIdx >= 23) return 0; // Out of scope. Only 0 - 23 is valid.

	return 0xFF + (SlotData[0xD6] * 0x6);

	/*
		If you instead want to access it directly from the SavData instead of the SlotData, rework it like this:
		Slot being '1' for Slot 1, '2' for Slot 2 etc.

		return (Slot * 0x1000) + 0xFF + (SavData[(Slot * 0x1000) + 0xD6] * 0x6);
	*/
};
```
<hr>


## Episode Table
You can find a list with the base offsets for each Episode below in the Table.

| Episode                | Start Offset |
| ---------------------- | ------------ |
| It All Began           | 0xFF         |
| Buried By the Mob      | 0x104        |
| Unofficial 1           | 0x109        |
| What Digs Beneath      | 0x10E        |
| Unofficial 2           | 0x113        |
| The Doomed Earth       | 0x118        |
| Blackout!              | 0x11D        |
| Aliens Arrived         | 0x122        |
| The New Cola           | 0x127        |
| Unofficial 3           | 0x12C        |
| A Brand New Scent      | 0x131        |
| Unofficial 4           | 0x136        |
| Unofficial 5           | 0x13B        |
| Triassic Trouble       | 0x140        |
| Unofficial 6           | 0x145        |
| There Was This Mummy   | 0x14A        |
| Unofficial 7           | 0x14F        |
| Unofficial 8           | 0x154        |
| Unofficial 9           | 0x159        |
| Unofficial 10          | 0x15E        |
| Unofficial 11          | 0x163        |
| A Very Special Reunion | 0x168        |
| It All Came to an End  | 0x16D        |
| Unofficial 12          | 0x172        |

<hr>


## Episode Rating
`0x0` up to `0x3` are the rating categories of the Episode.

The max value per rating category is `0x19` (25).

Below you will find a table with the index and what the category is.

| Category                | Index |
| ----------------------- | ----- |
| Plot Points Completed   | 0x0   |
| Aspiration Conversation | 0x1   |
| Hidden Want Completed   | 0x2   |
| Errand Completed        | 0x3   |

<hr>


## Episode Unlocked
The unlocked State is stored at bit index `0` at `0x4` of the Episode Structure.
<hr>


## Episode Played
The played State is stored at bit index `1` at `0x4` of the Episode Structure.
<hr>