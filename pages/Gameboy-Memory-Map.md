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
    <td></td>
    <td>0x9800 -> 0x9BFF (1KB)</td>
    <td>BG Map Data 1 (VRAM)</td>
  </tr>
  <tr>
    <td></td>
    <td>0x9C00 -> 0x9FFF (1KB)</td>
    <td>BG Map Data 2 (VRAM)</td>
  </tr>
  <tr>
    <td></td>
    <td>0xA000 -> 0xBFFF (8KB)</td>
    <td>Cartridge RAM (If Available)
(WRAM)</td>
  </tr>
  <tr>
    <td></td>
    <td>0xC000 - 0xCFFF (4KB)</td>
    <td>Internal RAM - Bank 0 (fixed)
(WRAM)</td>
  </tr>
  <tr>
    <td></td>
    <td>0xD000 -> 0xDFFF (4096 bytes)</td>
    <td>Internal RAM - Bank 1-7 (switchable - CGB only)</td>
  </tr>
  <tr>
    <td></td>
    <td>0xE000 -> 0xFDFF (7680 bytes)</td>
    <td>Echo RAM - Reserved, Do Not Use</td>
  </tr>
  <tr>
    <td>65024 -> 65183</td>
    <td>0xFE00 -> 0xFE9F (160 bytes)</td>
    <td>OAM - Object Attribute Memory</td>
  </tr>
  <tr>
    <td></td>
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
    <td>Zero Page</td>
  </tr>
  <tr>
    <td>65535</td>
    <td>0xFFFF (1 byte)</td>
    <td>Interrupt Enable Flag</td>
  </tr>
</table>


## Hardware I/O Registers (0xFF00 -> 0xFF7F) (128 bytes)

* ScrollY (0xFF42)

* ScrollX (0xFF43)

* WindowY (0xFF4A)

* WindowX (0xFF4B)

References: 

1. [http://gameboy.mongenel.com/dmg/asmmemmap.html](http://gameboy.mongenel.com/dmg/asmmemmap.html)  

