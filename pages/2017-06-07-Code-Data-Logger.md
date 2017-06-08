---
title: Code Data Logger (Emulation)
layout: post
author: amorri40
permalink: /code-data-logger/
tags:
- nes
- snes
- gameboy
- tools
- emulation
source-id: 1Akx1ob71e3q_DYen4HaaX0YRZlhboyPWZpLCh_QSmFU
published: true
---
# Code Data Logger (Emulation)

![image alt text]({{ site.url }}/public/IiA83YXfAzYaSGTnQsabPA_img_0.png)

### Purpose of the Code Data Logger

The Code/Data Logger makes it much easier to reverse-engineer NES ROMs. The basic idea behind it is that a normal NES disassembler cannot distinguish between code (which is executed) and data (which is read). The Code/Data Logger keeps track of what is executed and what is read while the game is played, and then you can save this information into a .cdl file, which is essentially a **mask** that tells which bytes in the ROM are code and which are data. The file can be used in conjunction with a suitable disassembler to disassemble only the actual game code, resulting in a much cleaner source code where code and data are properly separated.

### Uses for the Code Data Logger

* Creating a re-assemblable source code file using the cdl file to know exactly what each byte is used for (data or code)

* Easier to find unused resources in rom file - look for unmapped bytes after completing a whole game (e.g cutting-room-floor)

* Exodus emulator will properly identify the data as pointers and even form them into a table/array!

* Identify bytes that are being played as a sound

* Identify bytes that are being used as tilesets/sprites

* Know which bytes are unused to look for hidden gems, unused game assets

* Mark which byte is the first byte of an opcode to make more accurate disassembly listings

* Share files to get multiple people to help map out a rom

### CDL versus Trace Logging

* CDL is different than simply trace logging, in that you just care about how the rom is mapped out and a disassembly of it. Where as a trace logger is to give you an insight into what the registers and such, contain at the time of logging the disassembly. [1] 

### How Code/Data Logger works

* The CDL is mapped in real time, so you need to play the rom in an emulator from start to finish, to map it out. You need to do as much as possible: dieing, alternate paths, 2 players, secret areas etc

## CDL Tools

### Emulators that support CDL creation

* FCEUX - [http://www.fceux.com/web/help/fceux.html?CodeDataLogger.html](http://www.fceux.com/web/help/fceux.html?CodeDataLogger.html) 

* Bizhawk - 

* Exodus - [https://www.exodusemulator.com](https://www.exodusemulator.com) 

### Disassemblers that support CDL input

* IDA pro has a script which imports the cdl file and uses it to mark code and data bytes.

### Some complete cdl files

* [https://forums.sonicretro.org/index.php?showtopic=36572](https://forums.sonicretro.org/index.php?showtopic=36572) 

### Gameboy (Gambatte in Bizhawk)

* [https://github.com/TASVideos/BizHawk/blob/15a25bdd8763b3526b25e73406557cbb2305d2b0/BizHawk.Emulation.Cores/Consoles/Nintendo/Gameboy/Gambatte.ICodeDataLog.cs](https://github.com/TASVideos/BizHawk/blob/15a25bdd8763b3526b25e73406557cbb2305d2b0/BizHawk.Emulation.Cores/Consoles/Nintendo/Gameboy/Gambatte.ICodeDataLog.cs) (public partial class Gameboy : ICodeDataLogger) Only useful as an entry point

## Format of the Code data Logger

CDL files are just a mask of the ROM; that is, they are of the same size as the ROM, and each byte represents the corresponding byte of the ROM. The format of each byte is like so (in binary):

* The CDL format needs to be specific for the target system. 

    * Things like how the data was accessed in length, would be essential for Genesis (so instead of just 1 bit for data, use 2 bits - so you can know if the data was accessed as a byte, word, or long).

### FCEUX (NES) Format

#### For PRG ROM (8 bits in a byte):

<table>
  <tr>
    <td>Unused Bit</td>
    <td>Unused bit</td>
  </tr>
  <tr>
    <td>Audio Bit</td>
    <td>Used as Audio data</td>
  </tr>
  <tr>
    <td>Indirect Data Bit</td>
    <td>(e.g. as the destination of a JMP ($nnnn) instruction)</td>
  </tr>
  <tr>
    <td>Indirect Code Bit</td>
    <td>Whether indirectly accessed as data.
               (e.g. as the destination of an LDA ($nn),Y instruction)</td>
  </tr>
  <tr>
    <td>Rom Bank Bit1</td>
    <td>Into which ROM bank it was mapped when last accessed:
               00 = $8000-$9FFF        01 = $A000-$BFFF
               10 = $C000-$DFFF        11 = $E000-$FFFF</td>
  </tr>
  <tr>
    <td>RomBank Bit2</td>
    <td></td>
  </tr>
  <tr>
    <td>Data Bit</td>
    <td>The byte was executed as Data</td>
  </tr>
  <tr>
    <td>Code Bit</td>
    <td>The byte was executed as Code</td>
  </tr>
</table>


#### For CHR ROM:

<table>
  <tr>
    <td>Unused Bit</td>
    <td>Unused Bit</td>
  </tr>
  <tr>
    <td>Unused Bit</td>
    <td>Unused Bit</td>
  </tr>
  <tr>
    <td>Unused Bit</td>
    <td>Unused Bit</td>
  </tr>
  <tr>
    <td>Unused Bit</td>
    <td>Unused Bit</td>
  </tr>
  <tr>
    <td>Unused Bit</td>
    <td>Unused Bit</td>
  </tr>
  <tr>
    <td>Unused Bit</td>
    <td>Unused Bit</td>
  </tr>
  <tr>
    <td>Read Bit</td>
    <td>Whether it was read programmatically using port $2007
               (e.g. Argus_(J).nes checks if the bankswitching works by reading the same byte of CHR data before and after switching)
</td>
  </tr>
  <tr>
    <td>Drawn Bit</td>
    <td>Whether it was drawn on screen (rendered by PPU at runtime)</td>
  </tr>
</table>


### Implementation of a Code Data Logger

* The emulator creates a large Byte array, that's equal to the size of the rom. 

    * Each byte in the array corresponds to a byte in the rom address. So it's a map of the rom. 

        * Each bit in the byte represents how that data was accessed. For instance, Bit0= code, Bit1=data, Bit8= first byte of opcode. 

        * Other bits can represent how the data was accessed; directly, indirectly, indirectly for a jump table, etc. [1]

## References

1. **[Tomaitheous - details about format of CD**L](http://gendev.spritesmind.net/forum/memberlist.php?mode=viewprofile&u=83&sid=e08651c26032bd6aed6ed20888315ea5)

