---
layout: research
researchcategory: Internal
structure: sims2gba
title: Internal Menus
description: The Sims 2 Game Boy Advance | Internal Menu Research
permalink: /research/sims2gba/internal/menus
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.0.**
<hr>


## Technical information
***The game seems to be using function pointers to prepare, handle and terminate the Menus.***

***Here are some related addresses for the Menus.***

| Content                         | Address  |
| ------------------------------- | -------- |
| Current Menu ID                 | 03004720 |
| Backup Menu ID                  | 03004750 |
| New Menu ID                     | 03004770 |
| Base Function Pointer Prepare   | 08064F84 |
| Base Function Pointer Logic     | 08064F88 |
| Base Function Pointer Terminate | 08064F8C |

Basically, the game contains Menu IDs on the Internal Working RAM (IWRAM).

If `New Menu ID` is NOT the same as `Current Menu ID`, it seems to do the following things:

- Call the Terminate function of the current Menu.
- Backup the `Current Menu` Section into the `Backup Menu` Section `(0x20)`.
    - It looks like those are just backups, in case you'll cancel a specific Menu and the game then knows to what it should go back.
- Set the `New Menu` Section into the `Current Menu` Section `(0x20)`.
- Then call the Menu Prepare function to prepare the new Menu.

***If you are curious how to get the actual function start address, then here is how.***

- Note the value of: `Function Pointer + (MenuID * C)`.
    - Example with `MenuID` being `1A` and the Function Pointer `Prepare`: `08064F84 + (1A * C) => 080650BC`.
- Read 4 bytes of the address from above (if you want to do that while the game is running) or the result from above *minus* `08000000` (if you want to do that from the actual ROM).
    - Example with reading it from the ROM: `2D 56 03 08` => `0803562D` (The byte order needs to be swapped).

Now that result is the actual starting point, though for some reason it's 1 byte after the start it seems(?), so just do `- 0x1` and you are good to go.

If you want the ROM Location, just do `- 08000000` again and there you go. The Game Boy Advance stores the ROM at `08000000` in memory, that's why.
<hr>


## IDs
You can find a list of the Menu IDs below. Menus marked with `?? (Black screen)` still need to be figured out and some may black screen and eventually just freeze or crash the game if not used correctly.

| ID   | Menu                                                                           |
| ---- | ------------------------------------------------------------------------------ |
| 0x0  | ?? (Black screen)                                                              |
| 0x1  | In-Game                                                                        |
| 0x2  | The dialog Menu with all the options you can do in-game (such as "What's up?") |
| 0x3  | Intro #1                                                                       |
| 0x4  | Intro #2                                                                       |
| 0x5  | Main Menu with the Create-a-Sim, Load-a-Sim, ... Options                       |
| 0x6  | The Slot Loading Menu                                                          |
| 0x7  | ?? (Black screen)                                                              |
| 0x8  | Multi Player Link Connection                                                   |
| 0x9  | In-Game SELECT Menu                                                            |
| 0xA  | Language Selection                                                             |
| 0xB  | Plot Points Menu                                                               |
| 0xC  | Cast Member Menu                                                               |
| 0xD  | Social Action / Conversation Menu                                              |
| 0xE  | Inventory Menu                                                                 |
| 0xF  | Episode Selection Menu                                                         |
| 0x10 | Shop Menu                                                                      |
| 0x11 | Map                                                                            |
| 0x12 | ?? (Black screen)                                                              |
| 0x13 | ?? (Black screen)                                                              |
| 0x14 | Bigfoot Love Chickens                                                          |
| 0x15 | Car Commercial                                                                 |
| 0x16 | Message Box (Black screens if not used correctly)                              |
| 0x17 | Create-a-Sim Menu                                                              |
| 0x18 | Minigame Level Selection                                                       |
| 0x19 | Minigame results                                                               |
| 0x1A | Keelhaulin' Cards                                                              |
| 0x1B | Cattle Cleanup                                                                 |
| 0x1C | Let's watch the show!                                                          |
| 0x1D | Goth Family Let's watch the show!                                              |
| 0x1E | Options Menu with selecting an Episode etc                                     |
| 0x1F | King Chug Chug                                                                 |
| 0x20 | Canyon Jumping                                                                 |
| 0x21 | Credits                                                                        |
| 0x22 | Chop Shop                                                                      |
| 0x23 | Skills Menu                                                                    |
| 0x24 | Testing Menu(?)                                                                |
| 0x25 | Dusty Hogg motorbike sharkpool cutscene                                        |
| 0x26 | Game Ending cutscene                                                           |
| 0x27 | Minigames Menu                                                                 |

<hr>