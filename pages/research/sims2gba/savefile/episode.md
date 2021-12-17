---
layout: research
researchcategory: Savefile
structure: sims2gba
title: Episode
description: The Sims 2 Game Boy Advance | Episode Research
permalink: /research/sims2gba/savefile/episode
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.**
<hr>


## Some notes
- It is unknown yet, if `0x5` is the size for each episode exactly. See reason below.

The reason for that is, the episodes aren't stored like `0x0 - 0x4` first episode, `0x5 - 0x9` second episode etc.. instead it does have some other data between them in different sizes or maybe padding. Maybe that counts to the episodes as well? Not sure, that still has yet to be discovered.

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
	bool Unlocked = false; // Episode Unlocked State; 0x4.
};
```
<hr>


## Episode Offset
The Episode final offset depends on how many items you have in your House.

The amount of items you have in your house is stored at byte `0xD6` of the SavSlot's Data.

See below for a way how to get the final offset.

```cpp
static constexpr uint32_t EPOffsets[11] = {
	0x104, 0x10E, 0x122, // Season 1.
	0x11D, 0x131, 0x127, 0x14A, // Season 2.
	0x140, 0x118, 0x16D, 0x168 // Season 3.
};


/*
	SlotData is the data of the SavSlot.
	EPIdx is the episode index ( 0 - 10 ).

	The EPIdx has the index like the table below under Episode Tables, starting at 0 with "Buried By the Mob" and ending at 10 with "A Very Special Reunion".
*/
uint32_t GetOffset(uint8_t *SlotData, uint8_t EPIdx) {
	if (EPIdx >= 11) return 0; // Out of scope. Only 0 - 10 is valid.

	return EPOffsets[EPIdx] + (SlotData[0xD6] * 0x6);

	/*
		If you instead want to access it directly from the SavData instead of the SlotData, rework it like this:
		Slot being '1' for Slot 1, '2' for Slot 2 etc.

		return (Slot * 0x1000) + EPOffsets[EPIdx] + (SavData[(Slot * 0x1000) + 0xD6] * 0x6);
	*/
};
```
<hr>


## Episode Tables
You can find a list with the base offsets for each Episode below in the Table.

| Episode                | Start Offset |
| ---------------------- | ------------ |
| Buried By the Mob      | 0x104        |
| What Digs Beneath      | 0x10E        |
| Aliens Arrived         | 0x122        |
| Blackout!              | 0x11D        |
| A Brand New Scent      | 0x131        |
| The New Cola           | 0x127        |
| There Was This Mummy   | 0x14A        |
| Triassic Trouble       | 0x140        |
| The Doomed Earth       | 0x118        |
| It All Came to an End  | 0x16D        |
| A Very Special Reunion | 0x168        |

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
The unlocked State is literally just a boolean stored at `0x4` of the Episode Structure.

There isn't much to say about it except set it to `0x1` for Unlocked, `0x0` for Locked.
<hr>