---
layout: research
researchcategory: Internal
structure: sims2gba
title: Internal Keelhaulin' Cards Minigame
description: The Sims 2 Game Boy Advance | Internal Keelhaulin' Cards Minigame Research
permalink: /research/sims2gba/internal/keelhaulincards
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.2.**
<hr>


## TODOs
- Figure out how Player / Opponent cards are stored.
<hr>


## Notes
***Here are some related notes for the Keelhaulin' Cards Minigame.***

| Content                   | Size (hex) | Address  |
| ------------------------- | ---------- | -------- |
| Current Card Index        | 4(?)       | 03002074 |
| Card Deck Card Amount     | 1          | 03002398 |
| Player Card Amount        | 1          | 03002399 |
| Normal Type Played Flags  | 1          | 0300239A |
| Special Type Played Flags | 1          | 0300239B |
| Card Deck Start           | 30 - 3C    | 0300239C |
| Card Deck Index           | 1          | 030023D8 |
| Player Points             | 4          | 030023EC |
| Opponent Points           | 4          | 030023F0 |
| Treasure Points           | 4          | 030023F4 |
| Prepare Function          | 4          | 0803562C |
| Handler Function          | 4          | 080358EC |
| Terminate Function        | 4          | 0803769C |

<hr>


## Cardsets

**Normal Cards**

<img src="{{ "/assets/images/research/sims2gba/khc/card1.png" | absolute_url }}" alt="Normal Card 1">
<img src="{{ "/assets/images/research/sims2gba/khc/card2.png" | absolute_url }}" alt="Normal Card 2">
<img src="{{ "/assets/images/research/sims2gba/khc/card3.png" | absolute_url }}" alt="Normal Card 3">
<img src="{{ "/assets/images/research/sims2gba/khc/card4.png" | absolute_url }}" alt="Normal Card 4">
<img src="{{ "/assets/images/research/sims2gba/khc/card5.png" | absolute_url }}" alt="Normal Card 5">
<img src="{{ "/assets/images/research/sims2gba/khc/card6.png" | absolute_url }}" alt="Normal Card 6">
<img src="{{ "/assets/images/research/sims2gba/khc/card7.png" | absolute_url }}" alt="Normal Card 7">
<img src="{{ "/assets/images/research/sims2gba/khc/card8.png" | absolute_url }}" alt="Normal Card 8">

**Ghost Cards**

<img src="{{ "/assets/images/research/sims2gba/khc/card1_2.png" | absolute_url }}" alt="Ghost Card 1">
<img src="{{ "/assets/images/research/sims2gba/khc/card2_2.png" | absolute_url }}" alt="Ghost Card 2">
<img src="{{ "/assets/images/research/sims2gba/khc/card3_2.png" | absolute_url }}" alt="Ghost Card 3">
<img src="{{ "/assets/images/research/sims2gba/khc/card4_2.png" | absolute_url }}" alt="Ghost Card 4">
<img src="{{ "/assets/images/research/sims2gba/khc/card5_2.png" | absolute_url }}" alt="Ghost Card 5">
<img src="{{ "/assets/images/research/sims2gba/khc/card6_2.png" | absolute_url }}" alt="Ghost Card 6">
<img src="{{ "/assets/images/research/sims2gba/khc/card7_2.png" | absolute_url }}" alt="Ghost Card 7">
<img src="{{ "/assets/images/research/sims2gba/khc/card8_2.png" | absolute_url }}" alt="Ghost Card 8">

**Special Cards**

<img src="{{ "/assets/images/research/sims2gba/khc/card9.png" | absolute_url }}" alt="Special Card 1">
<img src="{{ "/assets/images/research/sims2gba/khc/card10.png" | absolute_url }}" alt="Special Card 2">
<img src="{{ "/assets/images/research/sims2gba/khc/card11.png" | absolute_url }}" alt="Special Card 3">

**Level 1**
- 5 cards of each Normal type.
- 1 card of each Ghost type.
- 0 cards of each Special type.
- `(5 * 8) + (1 * 8) + (0 * 3) => 48`

**Level 2**
- 5 cards of each Normal type.
- 1 card of each Ghost type.
- 4 cards of the first special card.
- `(5 * 8) + (1 * 8) + (1 * 4) => 52`

**Level 3**
- 5 cards of each Normal type.
- 1 card of each Ghost type.
- 4 cards of the first special card.
- `(5 * 8) + (1 * 8) + (1 * 4) => 52`

**Level 4**
- 5 cards of each Normal type.
- 1 card of each Ghost type.
- 4 cards of each Special type.
- `(5 * 8) + (1 * 8) + (3 * 4) => 60`

**Level 5**
- 5 cards of each Normal type.
- 1 card of each Ghost type.
- 4 cards of each Special type.
- `(5 * 8) + (1 * 8) + (3 * 4) => 60`

<hr>


## Card Deck
See above for the cardset the minigame contains per Level.

The minigame stores the cards from the card deck at `0300239C` up to the `030023D7` section. Depending on the Level you selected, it may use 48 cards, 52 cards or 60 cards.

You can find the amount of cards from the initialized card deck at `03002398`, and if you want to know what the next card of the card deck would be, you can find it at `030023D8`.

The cards from the card deck are 1 byte in size, as they just contain the card ID. The IDs are the following ones:

- 0 - 7: Normal cards from the displayed order above.
- 8 - F: Ghost cards from the displayed order above.
- 10 - 12: Special cards from the displayed order above.

After every draw of a card from the card deck, `Card Deck Index (030023D8)` will increase by 1.

Does the `Card Deck Index` reach `Card Deck Card Amount`, then the round will end after the Player lays down a card and gets the Treasure Points.
<hr>


## Flags
If a Ghost card can be played or not depends on the `Normal Type Played Flags`.

This contains a bitflag for all of the 8 normal type cards.

Are 3 or more of one Normal type card played, then the bit index of the Normal type index gets set to 1 and with that says: *You can now play the Ghost card of the specific card.*

There is also another bitflag which can be found on `Special Type Played Flags`, which sets the bits of the Special card indexes to 1, if it was used in that turn and if it's 1, you can't play that card for that turn anymore.
<hr>