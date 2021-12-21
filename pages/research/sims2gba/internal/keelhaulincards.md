---
layout: research
researchcategory: Internal
structure: sims2gba
title: Internal Keelhaulin' Cards Minigame
description: The Sims 2 Game Boy Advance | Internal Keelhaulin' Cards Minigame Research
permalink: /research/sims2gba/internal/keelhaulincards
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.1.**
<hr>

## TODOs
- Figure out how Player / Opponent cards are stored.
<hr>

## Technical Information
***Here are some related notes for the Keelhaulin' Cards Minigame.***

| Content               | Size (hex) | Address  |
| --------------------- | ---------- | -------- |
| Current Card Index    | 4(?)       | 03002074 |
| Player Points         | 4          | 030023EC |
| Opponent Points       | 4          | 030023F0 |
| Treasure Points       | 4          | 030023F4 |
| Card Deck Card Amount | 1          | 03002398 |
| Player Card Amount    | 4(?)       | 03002399 |
| Card Deck Start       | 30 - 3C    | 0300239C |
| Card Deck Index       | 1(?)       | 030023D8 |

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
- 5 Cards of each Normal type.
- 1 Card of each Ghost type.
- 0 Cards of each Special type.
- `(5 * 8) + (1 * 8) + (0 * 3) => 48`

**Level 2**
- TODO

**Level 3**
- TODO

**Level 4**
- TODO

**Level 5**
- 5 Cards of each Normal type.
- 1 Card of each Ghost type.
- 4 Cards of each Special type.
- `(5 * 8) + (1 * 8) + (4 * 3) => 60`

<hr>


## Card Deck
See above for the cardset the minigame contains per Level.

The minigame stores the cards from the card deck at `0300239C` up to the `030023D7` section. Depending on the Level it may just use 48 cards instead of all 60.

You can find the amount of cards from the initialized card deck at `03002398`, and if you want to know what the next card of the card deck would be, you can find it at `030023D8`.

The Cards from the card deck are 1 byte in size, as they just contain the card ID. The IDs are the following ones:

- 0 - 7: Normal Cards from the displayed order above.
- 8 - F: Ghost Cards from the displayed order above.
- 10 - 12: Special Cards from the displayed order above.

After every draw of a card from the card deck, `Card Deck Index (030023D8)` will increase by 1.

Does the `Card Deck Index` reach `Card Deck Card Amount`, then the round will end after the Player lays down a card and gets the Treasure Points.
<hr>