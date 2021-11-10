---
layout: research
researchcategory: Savefile
structure: sims2nds
title: Painting
description: The Sims 2 Nintendo DS | Painting Research
permalink: /research/sims2nds/painting
---

**Researched by [SuperSaiyajinStackZ](https://github.com/SuperSaiyajinStackZ), Version: 0.1.**
<hr>


## Some notes
- The first 5 bytes are always: `0x70, 0x74, 0x67, 0x0, 0xF` it seems.
- The Paintings start at `0x5000` of the Savefile.
- The Paintings have a size of `0x400`.
- There are 20 Paintings in the Savefile, so the range is: `0x5000 - 0x9FFF`.
- A Painting image is 48x32 pixels large.
- A byte contains a left and right pixel, so the first 4 bits is the left pixel, the second 4 bits the right pixel.
- There are 16 Palettes with 15 colors per palette.
- A pixel contains the index of the color from the specified palette.
- The first color of the palette in the pixel data starts at 1, so in case of an array which starts at 0, you have to do - 1.
- A Painting stores 2 checksums, one stored at `0xE - 0xF` (Header) and one stored at `0x10 - 0x11` (Main).
<hr>


## Structure
You can find a C++ structure for the Paintings below.

```cpp
/* The basic structure of the Painting. */
struct Painting {
	uint8_t Header[0x5] = { 0x70, 0x74, 0x67, 0x0, 0xF }; // "Painting" Header; 0x0 - 0x4.
	uint8_t Unknown1[0x3] = { 0x0 }; // Unknown. Maybe it's for the Header "Painting" as well?; 0x5 - 0x7.
	uint32_t PaintingIndex = 0x0; // Index of the Painting; 0x8 - 0xB.
	uint8_t Slot = 0x0; // The slot the painting is being part of; 0xC.
	uint8_t CanvasIndex = 0x0; // The index of the canvas in the art gallery ( 0 - 4 ) or favorite Painting ( 5 ); 0xD.
	uint16_t HeaderChecksum = 0x0; // Checksum of the Header; 0xE - 0xF.
	uint16_t MainChecksum = 0x0; // Checksum of the "Main"; 0x10 - 0x11.
	uint8_t Unknown2[0x2] = { 0x0 }; // Unknown; 0x12 - 0x13.
	uint8_t PaintingData[0x300] = { 0x0 }; // Painting Image Data; 0x14 - 0x313.
	uint8_t Flag = 0x0; // Flag of the Painting; 0x314.
	uint8_t Palette = 0x0; // The Palette Index; 0x315.
	uint8_t Unknown3[0xEA] = { 0x0 }; // Unknown; 0x316 - 0x3FF.
};


/* All English Painting "rank" names. */
const std::string RankNames[6] = {
	"Blank Canvas", "Garbage", "Ordinary", "Respectable", "Masterpiece", "Magnum Opus"
};


/*
	You need the colors of the Palettes? Then here you go.
	- There are 15 colors per palette.
	- There are 16 Palettes.
	The format of the palette is: R G B A in hexadecimal (uint32_t).
*/
static constexpr uint32_t Palette[] = {
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x000000FF, 0x00A0F8FF, 0x0078E0FF, 0x0048C8FF, 0x50F800FF, 0x28C000FF, 0x008000FF, 0xF8F800FF, 0xE8C800FF, 0xD09000FF, 0xF83038FF, 0xC00000FF,
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x484848FF, 0xA0D8F8FF, 0x80B8E0FF, 0x5898C8FF, 0xB8F898FF, 0x98D080FF, 0x78F890FF, 0xF8F890FF, 0xD8D070FF, 0xB8A850FF, 0xF8B8B8FF, 0xF89090FF,
	0xF8F8F8FF, 0x986820FF, 0x000000FF, 0xD000F8FF, 0x8828F8FF, 0x3070F8FF, 0x0090F8FF, 0x18A8A8FF, 0x38B850FF, 0x50D000FF, 0xA8E000FF, 0xF8E800FF, 0xF8B000FF, 0xF87800FF, 0xF84000FF,
	0xF8F8F8FF, 0x2880D8FF, 0x1898E0FF, 0x08B8F0FF, 0x00D0F8FF, 0x00B8A8FF, 0x00A850FF, 0x009800FF, 0xF8E070FF, 0xF8A858FF, 0xF87048FF, 0xF80828FF, 0xF890E0FF, 0xE878B0FF, 0xD06080FF,
	0xF8F8F8FF, 0xC0C8F8FF, 0x8898F8FF, 0x4068D8FF, 0x0038B8FF, 0xB8C000FF, 0xA0A800FF, 0x889000FF, 0x708000FF, 0x586800FF, 0xE0C098FF, 0xD08048FF, 0xC04000FF, 0x803000FF, 0x401800FF,
	0xF8F8F8FF, 0x78E8F8FF, 0x00D0F8FF, 0x00B8F8FF, 0x00A0F8FF, 0x80F000FF, 0x40D008FF, 0x00B010FF, 0x008008FF, 0x005800FF, 0xC89000FF, 0xB08000FF, 0x986800FF, 0x785800FF, 0x604000FF,
	0xF8F8F8FF, 0x808080FF, 0x000000FF, 0x00F8F8FF, 0x00A0A8FF, 0x004850FF, 0xC0F800FF, 0x80A800FF, 0x385000FF, 0xF84878FF, 0xA82850FF, 0x581028FF, 0xF820F8FF, 0xA820A8FF, 0x501850FF,
	0xF8F8F8FF, 0xB8B8B8FF, 0x000000FF, 0x18B8F8FF, 0x0898D0FF, 0x0078A8FF, 0xD0E878FF, 0x90B840FF, 0x508010FF, 0xF8B838FF, 0xC89018FF, 0xA07000FF, 0xF880A0FF, 0xF84878FF, 0x981030FF,
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x000000FF, 0xF8A090FF, 0xD87870FF, 0xB85848FF, 0x983028FF, 0xE0B078FF, 0xC8A068FF, 0xA88858FF, 0x907040FF, 0x90D890FF, 0x50B870FF, 0x10A058FF,
	0xF8F8F8FF, 0xA8A8A8FF, 0x505050FF, 0xE80040FF, 0xB00030FF, 0x780020FF, 0xB860F8FF, 0x8848C0FF, 0x603880FF, 0x403060FF, 0x0070D8FF, 0x0058A8FF, 0x004080FF, 0x002850FF, 0x000000FF,
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x484848FF, 0x000000FF, 0x98A8F8FF, 0x8080D8FF, 0x6060B8FF, 0x484090FF, 0x281870FF, 0xF8F878FF, 0xF0C038FF, 0xE88000FF, 0xE04000FF, 0xC00000FF,
	0xF8F8F8FF, 0xB07858FF, 0xA06040FF, 0x885028FF, 0x703818FF, 0x602800FF, 0xB08030FF, 0x906818FF, 0x685000FF, 0x5070A8FF, 0x303850FF, 0x100000FF, 0xF0C000FF, 0xD8A000FF, 0xC88000FF,
	0xF8F8F8FF, 0xF8D0A8FF, 0xE8B890FF, 0xD0A070FF, 0xB88050FF, 0xA06838FF, 0xF8E070FF, 0xE0A038FF, 0xC06000FF, 0x884000FF, 0x582000FF, 0x200000FF, 0x0068C8FF, 0x205090FF, 0x403860FF,
	0xF8F8F8FF, 0xE0F0F8FF, 0xC8E0F0FF, 0xB0D0E8FF, 0x98C0E0FF, 0x80B0E0FF, 0x68A0D8FF, 0x5090D0FF, 0x4880B8FF, 0x4070A8FF, 0x386090FF, 0x305078FF, 0x284060FF, 0x203050FF, 0x101828FF,
	0xF8F8F8FF, 0xF0E8D8FF, 0xE8D8B8FF, 0xE0C898FF, 0xD8B870FF, 0xD0A858FF, 0xC89840FF, 0xC08830FF, 0xB87818FF, 0xA87010FF, 0x986010FF, 0x805008FF, 0x704008FF, 0x583000FF, 0x482000FF,
	0xF8F8F8FF, 0xF0F0F0FF, 0xE0E0E0FF, 0xD0D0D0FF, 0xC0C0C0FF, 0xB0B0B0FF, 0xA0A0A0FF, 0x909090FF, 0x888888FF, 0x787878FF, 0x686868FF, 0x585858FF, 0x484848FF, 0x383838FF, 0x000000FF
};
```
<hr>


## Rankname

There are 6 Ranks, as you can also see on the structure, the ranks are:

| Name         | Range                                     |
| ------------ | ----------------------------------------- |
| Blank Canvas | Every first value of 2.                   |
| Garbage      | Every second value of 2 from 0x0 - 0x7.   |
| Ordinary     | Every second value of 2 from 0x8 - 0xF.   |
| Respectable  | Every second value of 2 from 0x10 - 0x17. |
| Masterpiece  | Every second value of 2 from 0x18 - 0x1F. |
| Magnum Opus  | Every second value of 2 from 0x20 - 0x27. |


Below you will find an example how to get the rank name.

```cpp
const std::string RankNames[6] = {
	"Blank Canvas", "Garbage", "Ordinary", "Respectable", "Masterpiece", "Magnum Opus"
};

std::string GetRank(const uint8_t Flag) {
	if (Flag >= 0x29) return "?"; // 0x29+ is out of scope. Only range 0x0 - 0x28 is valid.

	/*
		Each "Rank" has a range of 8, so we need to do " / 8", to get the rank name.
		We do "1 +" because the actual first "category" in our RankNames strings is index 1.
	*/
	const uint8_t Category = 1 + (Flag / 8); // The categories are calculated like this i assume.

	/*
		The game handles each first of two being a "Blank Canvas", that's why we check for:
		"Flag % 2 == 0", which basically means, check each first value of 2.

		std::min is mostly for ensureness.
	*/
	return (Flag % 2 == 0 ? RankNames[0] : RankNames[std::min<uint8_t>(5, Category)]);
};
```
<hr>


## ImageData Pixels

The image data start at byte `0x14` and go up to `0x313`.

One byte contains a left and a right pixel, while the first 4 bits are the left pixel and the second 4 bits are the right pixel.

Below you can find an example how to get a pixel from an index (ignoring left and right as one), so you can get them as you want.

The following palette has the color format: R G B A in hexadecimal as an uint32_t.

There are 16 Palettes with 15 colors each.

```cpp
static constexpr uint32_t Palette[] = {
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x000000FF, 0x00A0F8FF, 0x0078E0FF, 0x0048C8FF, 0x50F800FF, 0x28C000FF, 0x008000FF, 0xF8F800FF, 0xE8C800FF, 0xD09000FF, 0xF83038FF, 0xC00000FF,
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x484848FF, 0xA0D8F8FF, 0x80B8E0FF, 0x5898C8FF, 0xB8F898FF, 0x98D080FF, 0x78F890FF, 0xF8F890FF, 0xD8D070FF, 0xB8A850FF, 0xF8B8B8FF, 0xF89090FF,
	0xF8F8F8FF, 0x986820FF, 0x000000FF, 0xD000F8FF, 0x8828F8FF, 0x3070F8FF, 0x0090F8FF, 0x18A8A8FF, 0x38B850FF, 0x50D000FF, 0xA8E000FF, 0xF8E800FF, 0xF8B000FF, 0xF87800FF, 0xF84000FF,
	0xF8F8F8FF, 0x2880D8FF, 0x1898E0FF, 0x08B8F0FF, 0x00D0F8FF, 0x00B8A8FF, 0x00A850FF, 0x009800FF, 0xF8E070FF, 0xF8A858FF, 0xF87048FF, 0xF80828FF, 0xF890E0FF, 0xE878B0FF, 0xD06080FF,
	0xF8F8F8FF, 0xC0C8F8FF, 0x8898F8FF, 0x4068D8FF, 0x0038B8FF, 0xB8C000FF, 0xA0A800FF, 0x889000FF, 0x708000FF, 0x586800FF, 0xE0C098FF, 0xD08048FF, 0xC04000FF, 0x803000FF, 0x401800FF,
	0xF8F8F8FF, 0x78E8F8FF, 0x00D0F8FF, 0x00B8F8FF, 0x00A0F8FF, 0x80F000FF, 0x40D008FF, 0x00B010FF, 0x008008FF, 0x005800FF, 0xC89000FF, 0xB08000FF, 0x986800FF, 0x785800FF, 0x604000FF,
	0xF8F8F8FF, 0x808080FF, 0x000000FF, 0x00F8F8FF, 0x00A0A8FF, 0x004850FF, 0xC0F800FF, 0x80A800FF, 0x385000FF, 0xF84878FF, 0xA82850FF, 0x581028FF, 0xF820F8FF, 0xA820A8FF, 0x501850FF,
	0xF8F8F8FF, 0xB8B8B8FF, 0x000000FF, 0x18B8F8FF, 0x0898D0FF, 0x0078A8FF, 0xD0E878FF, 0x90B840FF, 0x508010FF, 0xF8B838FF, 0xC89018FF, 0xA07000FF, 0xF880A0FF, 0xF84878FF, 0x981030FF,
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x000000FF, 0xF8A090FF, 0xD87870FF, 0xB85848FF, 0x983028FF, 0xE0B078FF, 0xC8A068FF, 0xA88858FF, 0x907040FF, 0x90D890FF, 0x50B870FF, 0x10A058FF,
	0xF8F8F8FF, 0xA8A8A8FF, 0x505050FF, 0xE80040FF, 0xB00030FF, 0x780020FF, 0xB860F8FF, 0x8848C0FF, 0x603880FF, 0x403060FF, 0x0070D8FF, 0x0058A8FF, 0x004080FF, 0x002850FF, 0x000000FF,
	0xF8F8F8FF, 0xC0C0C0FF, 0x808080FF, 0x484848FF, 0x000000FF, 0x98A8F8FF, 0x8080D8FF, 0x6060B8FF, 0x484090FF, 0x281870FF, 0xF8F878FF, 0xF0C038FF, 0xE88000FF, 0xE04000FF, 0xC00000FF,
	0xF8F8F8FF, 0xB07858FF, 0xA06040FF, 0x885028FF, 0x703818FF, 0x602800FF, 0xB08030FF, 0x906818FF, 0x685000FF, 0x5070A8FF, 0x303850FF, 0x100000FF, 0xF0C000FF, 0xD8A000FF, 0xC88000FF,
	0xF8F8F8FF, 0xF8D0A8FF, 0xE8B890FF, 0xD0A070FF, 0xB88050FF, 0xA06838FF, 0xF8E070FF, 0xE0A038FF, 0xC06000FF, 0x884000FF, 0x582000FF, 0x200000FF, 0x0068C8FF, 0x205090FF, 0x403860FF,
	0xF8F8F8FF, 0xE0F0F8FF, 0xC8E0F0FF, 0xB0D0E8FF, 0x98C0E0FF, 0x80B0E0FF, 0x68A0D8FF, 0x5090D0FF, 0x4880B8FF, 0x4070A8FF, 0x386090FF, 0x305078FF, 0x284060FF, 0x203050FF, 0x101828FF,
	0xF8F8F8FF, 0xF0E8D8FF, 0xE8D8B8FF, 0xE0C898FF, 0xD8B870FF, 0xD0A858FF, 0xC89840FF, 0xC08830FF, 0xB87818FF, 0xA87010FF, 0x986010FF, 0x805008FF, 0x704008FF, 0x583000FF, 0x482000FF,
	0xF8F8F8FF, 0xF0F0F0FF, 0xE0E0E0FF, 0xD0D0D0FF, 0xC0C0C0FF, 0xB0B0B0FF, 0xA0A0A0FF, 0x909090FF, 0x888888FF, 0x787878FF, 0x686868FF, 0x585858FF, 0x484848FF, 0x383838FF, 0x000000FF
};


/*
	PaintingBuffer is the buffer of the Painting.
	Idx is the pixel index (not counting left and right as a single one).
*/
uint32_t GetPixel(uint8_t *PaintingBuffer, const uint16_t Idx) {
	if (Idx >= 0x600) return Palette[0]; // 0x600+ is out of scope already. 0x0 - 0x5FF is valid.

	const uint8_t Palette = PaintingBuffer[0x315]; // Get the palette from byte 0x315.

	/* Now get the pixel index. The image data starts at 0x14 of the painting. */
	uint8_t PixelIdx = 0;

	/* "Idx % 2 == 0" is the Left pixel. */
	if (Idx % 2 == 0)	PixelIdx = (PaintingBuffer[0x14 + (Idx / 2)] & 0xF); // Left pixel.
	/* If it's "Idx % 2 == 1", then it's the Right pixel. */
	else				PixelIdx = (PaintingBuffer[0x14 + (Idx / 2)] >> 0x4); // Right pixel.

	/*
		Now what we do is the following:

		Because the first color index is "1", we have to subtract 1 from the PixelIdx, because an array starts at 0.
		We also really need to do a std::max call, because we can potential underflow, when the PixelIdx is 0, then.

		Then we add the Palette Index times 15 (for the amount of colors per palette).

		Now we got our pixel as R G B A!
	*/
	return Palette[std::max<uint8_t>(0, (PixelIdx - 1)) + (Palette * 15)];
};

/*
	Here get them with an X and Y Position.

	PaintingBuffer is the buffer of the Painting.
	X is the X Position of the Painting. (47 is the max).
	Y is the Y Position of the Painting. (31 is the max).
*/
uint32_t GetPixelPos(uint8_t *PaintingBuffer, const uint8_t X, const uint8_t Y) {
	if (Y >= 32 || X >= 48) return Palette[0]; // Out of range.

	return GetPixel(PaintingBuffer, (Y * 48) + X);
};
```
<hr>


## Slot

There are 3 Slots you can use in game. The first Slot is `0`, the second Slot is `1` and the third Slot is `2`.

The Slot index is stored at `0xC` in the Header of the Painting.
<hr>


## Canvas Index

There are 5 Canvas in the art gallery and 1 wherever you place your "favorite" Painting. Here are the values for each listed.

| Where                              | Value |
| ---------------------------------- | ----- |
| Art Gallery bottom left            | 0x0   |
| Art Gallery top left               | 0x1   |
| Art Gallery top middle             | 0x2   |
| Art Gallery top right              | 0x3   |
| Art Gallery bottom right           | 0x4   |
| Wherever your favorite Painting is | 0x5   |

The index is stored at `0xD` in the Header of the Painting.
<hr>


## Painting Checksum

Of course the Painting also stores checksums, 2 to be exact.

There are 2 checksums, one stored at `0xE - 0xF` (The Header) and one at `0x10 - 0x11` (The Main).

Below you can find a C++ way to fix both Checksums, if they are invalid.

```cpp
/*
	PaintingBuffer is the buffer of the Painting.
*/
void UpdateChecksum(uint8_t *PaintingBuffer) {
	/* Calculate the main Checksum (0x10 - 0x11). */
	uint8_t Byte1 = 0, Byte2 = 0;

	for (uint16_t Idx = (0x10 / 2); Idx < (0x400 / 2); Idx++) {
		if (Idx == (0x10 / 2)) continue; // We are skipping the checksum here for the calculation.

		if (PaintingBuffer[Idx * 2] + Byte1 > 255) Byte2++;

		Byte1 += PaintingBuffer[Idx * 2];
		Byte2 += PaintingBuffer[(Idx * 2) + 1];
	}

	Byte2++;

	uint16_t Calced = (256 * (uint8_t)-Byte2) + (uint8_t)-Byte1;
	uint16_t CurChks = *reinterpret_cast<uint16_t *>(PaintingBuffer + 0x10);
	if (CurChks != Calced) *reinterpret_cast<uint16_t *>(PaintingBuffer + 0x10) = Calced;


	/* Now do the same for the Header (0xE - 0xF). */
	Byte1 = 0, Byte2 = 0; // Reset.

	for (uint16_t Idx = 0; Idx < (0x13 / 2); Idx++) {
		if (Idx == (0xE / 2)) continue; // We are skipping the checksum here for the calculation.

		if (PaintingBuffer[Idx * 2] + Byte1 > 255) Byte2++;

		Byte1 += PaintingBuffer[Idx * 2];
		Byte2 += PaintingBuffer[(Idx * 2) + 1];
	}

	Byte2++;

	Calced = (256 * (uint8_t)-Byte2) + (uint8_t)-Byte1;
	CurChks = *reinterpret_cast<uint16_t *>(PaintingBuffer + 0xE);
	if (CurChks != Calced) *reinterpret_cast<uint16_t *>(PaintingBuffer + 0xE) = Calced;
};
```
<hr>


## Fixing corrupted Painting

If you started the game with an invalid checksum on the paintings, the game formats the Header of the Painting, to make it not usable. However, there is an easy way to fix the corruption, as long as you remember a few details:

- What was the Index before stored at `0x8`?
- What was the Slot the Painting was for stored at `0xC`?
- What was the Canvas index the Painting was stored at `0xD`?

You can detect, if the Painting got formatted, when the first 0x14 bytes look like this:
```
2A 2A 2A 00 00 00 00 00 E0 20 7E 02 D8 8F 00 00 00 00 00 00
```

If you know all of them, then you should be good to fix that, below there's an implementation in C++ how to fix them.

```cpp
void FixPainting(uint8_t *PaintingBuffer, const uint32_t Index, const uint8_t Slot, const uint8_t CanvasIdx) {
	/* Fix Header Identifier 0x0 - 0x4. */
	PaintingBuffer[0x0] = 'p'; PaintingBuffer[0x1] = 't'; PaintingBuffer[0x2] = 'g'; PaintingBuffer[0x3] = 0x0; PaintingBuffer[0x4] = 0xF;

	/* TODO: Figure out what 0x5 - 0x7 is, for now have it as 0x0. */
	for (uint8_t Idx = 0; Idx < 3; Idx++) PaintingBuffer[0x5 + Idx] = 0x0;

	/* Set the Index at 0x8 - 0xB (uint32_t). */
	*reinterpret_cast<uint32_t *>(PaintingBuffer + 0x8) = Index;

	/* Set the Slot at 0xC. */
	PaintingBuffer[0xC] = Slot;

	/* Set the Canvas Index at 0xD. */
	PaintingBuffer[0xD] = CanvasIdx;

	/* Checksum needs to be calculated (0xE - 0xF AND 0x10 - 0x11) with the method "UpdateChecksum" above.. but at the end! */

	/* TODO: Figure out what 0x12 - 0x13 is, for now have it as 0x0. */
	for (uint8_t Idx = 0; Idx < 2; Idx++) PaintingBuffer[0x12 + Idx] = 0x0;

	/*
		NOW: Update the main checksum (0x10 - 0x11) first with the method "UpdateChecksum", then the Header with 0xE - 0xF.
		The method above handles both properly into one.
	*/
};
```
<hr>