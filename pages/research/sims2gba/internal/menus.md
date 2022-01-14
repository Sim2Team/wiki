---
layout: research
researchcategory: Internal
structure: sims2gba
title: Internal Menus
description: The Sims 2 Game Boy Advance | Internal Menu Research
permalink: /research/sims2gba/internal/menus
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.1.**
<hr>


## Notes
***Here are some related notes for the Internal Menus.***

| Content                         | Address  |
| ------------------------------- | -------- |
| Active Menu ID                  | 03004720 |
| Last Menu ID                    | 03004750 |
| New Menu ID                     | 03004770 |
| Base Function Pointer Init      | 08064F84 |
| Base Function Pointer Handler   | 08064F88 |
| Base Function Pointer Terminate | 08064F8C |

<hr>


## Technical Information
As listed on the Notes Section, there are 3 Menu IDs, `Active Menu`, `Last Menu` and `New Menu`.

The `Active Menu` has the following Section:
- `03004720 - 0300473F`

The `Last Menu` has the following Section:
- `03004750 - 0300476F`

The `New Menu` has the following Section:
- `03004770 - 0300478F`

In all cases, the first 4 bytes is the `Menu ID` (See below for the IDs).

Then it looks like each following 4 bytes are the Arguments. Like `03004774 - 03004777` is Argument 1, `03004778 - 0300477B` is Argument 2 etc..

***If switched to a new Menu***

- Set the New Menu ID + Arguments into 03004770, 03004774, 03004778 ....
- Fade the screen out (Depends on the Menu).
- Terminate the Active Menu.
- Backup the Active Menu to 03004750 + Arguments to the Last Menu, then set the New Menu ID + Arguments into 03004720 (the Active Menu).
- Initialize the New Menu.
- Fade the screen in (Depends on the Menu).


***If you are curious how to get the actual function start address, then here is how.***

- Note the value of: `Function Pointer + (MenuID * C)`.
    - Example with `MenuID` being `1A` and the Function Pointer `Init`: `08064F84 + (1A * C) => 080650BC`.
- Read 4 bytes of the address from above.
    - Example with reading it from the ROM: `2D 56 03 08` => `0803562D` (The byte order needs to be swapped).
<hr>


## IDs
You can find a list of the Menu IDs below.

| ID   | Menu                                                                           |
| ---- | ------------------------------------------------------------------------------ |
| 0x0  | Unused (just does bx lr)                                                       |
| 0x1  | In-Game                                                                        |
| 0x2  | The dialog Menu with all the options you can do in-game (such as "What's up?") |
| 0x3  | Intro #1 (Copyright Scene)                                                     |
| 0x4  | Intro #2 (EA + Maxis brand Scene)                                              |
| 0x5  | Main Menu with the Create-a-Sim, Load-a-Sim, ... Options                       |
| 0x6  | The Slot Loading Menu                                                          |
| 0x7  | Unused (just does bx lr)                                                       |
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
| 0x12 | Unused (just does bx lr)                                                       |
| 0x13 | Unused (just does bx lr)                                                       |
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


## Social Action / Conversation Menu (0xD)
Some more Information about the Social Action / Conversation Menu.

| Parameter               | Address  |
| ----------------------- | -------- |
| Conversation Type       | 03004774 |
| Conversation Partner ID | 03004778 |


***Conversation Type***

The Conversation types are literally the following:
- 0x0 => Friendly Conversation
- 0x1 => Romance Conversation
- 0x2 => Intimidate Conversation

Everything above that from a first view seems to freeze.


***Conversation Partner ID***

Here is a list of the Partner IDs.

| Partner                       | ID  |
| ----------------------------- | --- |
| Misty Waters                  | 0   |
| Misty Waters                  | 1   |
| Misty Waters                  | 2   |
| Bugged Tank Grunt             | 3   |
| Casino Keelhaulin' Cards Guy  | 4   |
| Collectibles Buyer            | 5   |
| Johnny Smith                  | 6   |
| Misty Waters                  | 7   |
| Misty Waters                  | 8   |
| Misty Waters                  | 9   |
| Saloon Girl                   | A   |
| Daddy Bigbucks                | B   |
| Skillbook Seller              | C   |
| Emperor Xizzle                | D   |
| Burple                        | E   |
| Ara Fusilli                   | F   |
| Auda Sherif                   | 10  |
| Ava Cadavra                   | 11  |
| Bigfoot                       | 12  |
| Frankie Fusilli               | 13  |
| Dusty Hogg                    | 14  |
| Giuseppi Mezzoalto            | 15  |
| Honest Jackson                | 16  |
| Jebediah Jerky                | 17  |
| Jimmy the Neck                | 18  |
| Kayleigh Wintercrest          | 19  |
| Luthor L. Bigbucks            | 1A  |
| Mamma Hogg                    | 1B  |
| Misty Waters                  | 1C  |
| Lord Mole                     | 1D  |
| Mummy                         | 1E  |
| Optimum Alfred                | 1F  |
| Penelope Redd                 | 20  |
| Pepper Pete                   | 21  |
| Kent Hackett                  | 22  |
| Sancho Paco Panza             | 23  |
| Tank Grunt                    | 24  |
| Tristan Legend                | 25  |
| Yeti                          | 26  |
| Burple (Toilet version)       | 27  |
| Emperor Xizzle (Invisible)    | 28  |

0x0 - 0xC seem to be some test cases or so, while 0xD - 0x26 are the actual valid IDs which the game sets.

0x27 and 0x28 are sorta test cases too(?).

0x29 and up just seem to freeze.


***For more internal working to the Social Action / Conversation Menu, check out the <a href="{{ "/research/sims2gba/internal/socialactionmenu" | absolute_url }}">Social Action / Conversation Page</a>.***
<hr>


## Shop Menu (0x10)
Some more Information about the Shop Menu.

| Parameter               | Address  |
| ----------------------- | -------- |
| Shop ID                 | 03004778 |

**There may be more Parameters, but so far only this one seems to be related.**

***Shop ID***

Here is a list of the Shop IDs.

| Shop             | ID  |
| ---------------- | --- |
| Pawn Shop        | 0   |
| Saloon           | 1   |
| Skills           | 2   |
| Collectibles     | 3   |
| Mailbox          | 4   |

IDs above may re-use the Shop's on the list.. or eventually crash.
<hr>