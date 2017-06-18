---
title: Gameboy Memory Map
layout: post
author: amorri40
permalink: /gameboy-memory-map/
tags:
- gameboy
- emulation
- memory
- nintendo
source-id: 17ogTZ-xdyCcJ60M6qFyhdGF5PQ9VlHgeNyr4bCqzpCg
published: true
---
## Gameboy Hardware

CPU: 8-bit

Address Bus: 16-bit

Total Memory Addresses: 65,536 (0x10000) (64KB)

### Why only 65536 addresses?

"The GameBoy contains an 8-bit processor, meaning it can access 8-bits of data at one time. To access this data, it has a 16-bit address bus, which can address 65,536 positions of memory" [1].

# Memory Map

<table>
  <tr>
    <td>Address Range (dec) </td>
    <td>Address Range (hex) </td>
    <td>Purpose of Memory</td>
  </tr>
  <tr>
    <td>0 -> 255</td>
    <td>0x0000 -> 0x00FF (255 bytes)</td>
    <td>Restart and Interrupt Vectors</td>
  </tr>
  <tr>
    <td>256 -> 335</td>
    <td>0x0100 -> 0x014F (80 bytes)</td>
    <td>Cartridge Header Area</td>
  </tr>
  <tr>
    <td>336 -> 16383</td>
    <td>0x0150 -> 0x3FFF (16KB)</td>
    <td>Cartridge ROM - Bank 0 (fixed)</td>
  </tr>
  <tr>
    <td>16384 -> 32767</td>
    <td>0x4000 -> 0x7FFF (16KB)</td>
    <td>Cartridge ROM - Switchable Banks 1-xx</td>
  </tr>
  <tr>
    <td>32768 -> 38911</td>
    <td>0x8000 -> 0x97FF (6KB)</td>
    <td>Character RAM (VRAM)</td>
  </tr>
  <tr>
    <td>38912 -> 39935</td>
    <td>0x9800 -> 0x9BFF (1KB)</td>
    <td>BG Map Data 1 (VRAM)</td>
  </tr>
  <tr>
    <td>39936 -> 40959</td>
    <td>0x9C00 -> 0x9FFF (1KB)</td>
    <td>BG Map Data 2 (VRAM)</td>
  </tr>
  <tr>
    <td>40960 -> 49151</td>
    <td>0xA000 -> 0xBFFF (8KB)</td>
    <td>Cartridge RAM (If Available)
(WRAM)</td>
  </tr>
  <tr>
    <td>49152 -> 53247</td>
    <td>0xC000 - 0xCFFF (4KB)</td>
    <td>Internal RAM - Bank 0 (fixed)
(WRAM)</td>
  </tr>
  <tr>
    <td>53248 -> 57343</td>
    <td>0xD000 -> 0xDFFF (4096 bytes)</td>
    <td>Internal RAM - Bank 1-7 (switchable - CGB only)</td>
  </tr>
  <tr>
    <td>57344 -> 65023</td>
    <td>0xE000 -> 0xFDFF (7680 bytes)</td>
    <td>Echo RAM - Reserved, Do Not Use</td>
  </tr>
  <tr>
    <td>65024 -> 65183</td>
    <td>0xFE00 -> 0xFE9F (160 bytes)</td>
    <td>OAM - Object Attribute Memory</td>
  </tr>
  <tr>
    <td>65184 -> 65279</td>
    <td>0xFEA0 -> 0xFEFF (96 bytes)</td>
    <td>Unusable Memory</td>
  </tr>
  <tr>
    <td>65280 -> 65407</td>
    <td>0xFF00 -> 0xFF7F (128 bytes)</td>
    <td>Hardware I/O Registers</td>
  </tr>
  <tr>
    <td>65408 -> 65534</td>
    <td>0xFF80 -> 0xFFFE (127 bytes)</td>
    <td>Zero Page (HRAM / HiRam)</td>
  </tr>
  <tr>
    <td>65535</td>
    <td>0xFFFF (1 byte)</td>
    <td>Interrupt Enable Flag</td>
  </tr>
</table>


## OAM - Object Attribute memory (Sprites)

**Size of memory**: 160 Bytes

**Number of Sprites**: 40

**Size of Sprites**: 8x8 or 8x16

"On the Gameboy the OAM is a 160-byte long chunk of memory, and each sprite takes up 4 bytes which leaves just enough room for exactly 40 sprite.

We can not access it while the display is updating (Which is a lot of the time!). This is where the so-called Direct Memory Access (DMA) comes into play." [2].

<table>
  <tr>
    <td>Y</td>
    <td>Location of Sprite on Screen from top to bottom</td>
  </tr>
  <tr>
    <td>X</td>
    <td>Location of Sprite on Screen from left to right</td>
  </tr>
  <tr>
    <td>Tile Number</td>
    <td>Tile in the tile-map to use to render this sprite</td>
  </tr>
  <tr>
    <td>Flags</td>
    <td>Flag values:
7: Render priority6: Y flip5: X flip4: Palette number       (GB Color only)3: VRAM bank            (GB Color only)2: Palette number bit 3 (GB Color only)1: Palette number bit 2 (GB Color only)0: Palette number bit 1 (GB Color only)</td>
  </tr>
</table>


## Hardware I/O Registers (0xFF00 -> 0xFF7F) (128 bytes)

<table>
  <tr>
    <td>0xFF42</td>
    <td>ScrollY</td>
  </tr>
  <tr>
    <td>0xFF43</td>
    <td>ScrollX</td>
  </tr>
  <tr>
    <td>0xFF44</td>
    <td>LY - LCDC Y-Coordinate (Read-only)</td>
  </tr>
  <tr>
    <td>0xFF45</td>
    <td>LYC - LY Compare (Read/Write)</td>
  </tr>
  <tr>
    <td>0xFF46</td>
    <td>DMA - DMA Transfer and Start Address (Write-only)</td>
  </tr>
  <tr>
    <td>0xFF47</td>
    <td>BGP - BG Palette Data (Read/Write) - Non CGB Mode Only</td>
  </tr>
  <tr>
    <td>0xFF48</td>
    <td>OBP0 - Object Palette 0 Data (R/W) - Non CGB Mode Only</td>
  </tr>
  <tr>
    <td>0xFF49</td>
    <td>OBP1 - Object Palette 1 Data (R/W) - Non CGB Mode Only</td>
  </tr>
  <tr>
    <td>0xFF4A</td>
    <td>WindowY</td>
  </tr>
  <tr>
    <td>0xFF4B</td>
    <td>WindowX</td>
  </tr>
  <tr>
    <td>0xFF4C</td>
    <td>??</td>
  </tr>
  <tr>
    <td>0xFF4D</td>
    <td>KEY1 - CGB Mode Only - Prepare Speed Switch</td>
  </tr>
  <tr>
    <td>0xFF4E</td>
    <td>??</td>
  </tr>
  <tr>
    <td>0xFF4F</td>
    <td>VBK - CGB Mode Only - VRAM Bank</td>
  </tr>
  <tr>
    <td>0xFF50</td>
    <td>Locks Bootrom</td>
  </tr>
  <tr>
    <td>0xFF51 -> 0xFF55</td>
    <td>LCD VRAM DMA Transfers (CGB only)</td>
  </tr>
  <tr>
    <td>0xFF56</td>
    <td>RP - CGB Mode Only - Infrared Communications Port</td>
  </tr>
  <tr>
    <td>0xFF57 -> 0xFF67</td>
    <td>??</td>
  </tr>
  <tr>
    <td>0xFF68</td>
    <td>BCPS/BGPI - CGB Mode Only - Background Palette Index</td>
  </tr>
  <tr>
    <td>0xFF69</td>
    <td>BCPD/BGPD - CGB Mode Only - Background Palette Data</td>
  </tr>
  <tr>
    <td>0xFF6A</td>
    <td>OCPS/OBPI - CGB Mode Only - Sprite Palette Index</td>
  </tr>
  <tr>
    <td>0xFF6B</td>
    <td>OCPD/OBPD - CGB Mode Only - Sprite Palette Data</td>
  </tr>
  <tr>
    <td>0xFF6C -> 0xFF6F</td>
    <td>??</td>
  </tr>
  <tr>
    <td>0xFF70</td>
    <td>FF70 - SVBK - CGB Mode Only - WRAM Bank</td>
  </tr>
  <tr>
    <td>0xFF71 -> FF7F</td>
    <td>??</td>
  </tr>
</table>


References: 

1. [http://gameboy.mongenel.com/dmg/asmmemmap.html](http://gameboy.mongenel.com/dmg/asmmemmap.html)  

2. [http://exez.in/gameboy-dma](http://exez.in/gameboy-dma) 

