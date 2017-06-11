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

* Bizhawk - [http://tasvideos.org/Bizhawk/CodeDataLogger.html](http://tasvideos.org/Bizhawk/CodeDataLogger.html) 

* Exodus - [https://www.exodusemulator.com](https://www.exodusemulator.com) 

### Disassemblers that support CDL input

* IDA pro has a script which imports the cdl file and uses it to mark code and data bytes.

### Some complete cdl files

* [https://forums.sonicretro.org/index.php?showtopic=36572](https://forums.sonicretro.org/index.php?showtopic=36572) 

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


### Bizhawk Format (Multi-system)

The Bizhawk CodeDataLogger supports multiple emulation cores but always follows a fairly common structure:

![image alt text]({{ site.url }}/public/IiA83YXfAzYaSGTnQsabPA_img_1.png)

<table>
  <tr>
    <td>Number in Screenshot</td>
    <td>Name of Section</td>
    <td>Example Value</td>
  </tr>
  <tr>
    <td>1</td>
    <td>File identifier</td>
    <td>"BIZHAWK-CDL-2"</td>
  </tr>
  <tr>
    <td>2</td>
    <td>Platform name</td>
    <td>"Gen", “GB”</td>
  </tr>
  <tr>
    <td>3</td>
    <td>Number of blocks (e.g ROM, WRAM..)</td>
    <td>3</td>
  </tr>
  <tr>
    <td>4</td>
    <td>Name of Block</td>
    <td>MD Cart (Megadrive cartridge)</td>
  </tr>
  <tr>
    <td>5</td>
    <td>Number of bytes in block</td>
    <td>4MB</td>
  </tr>
  <tr>
    <td>6</td>
    <td>Block data</td>
    <td>00, 01, 04, 40 </td>
  </tr>
</table>


### Implementation of a Code Data Logger

* The emulator creates a large Byte array, that's equal to the size of the rom. 

    * Each byte in the array corresponds to a byte in the rom address. So it's a map of the rom. 

        * Each bit in the byte represents how that data was accessed. For instance, Bit0= code, Bit1=data, Bit8= first byte of opcode. 

        * Other bits can represent how the data was accessed; directly, indirectly, indirectly for a jump table, etc. [1]

    * So after loading the rom, allocate a byte array the same size as the rom loaded and set all bytes to 0

        * Every time a opcode is executed flip the bit

        * Every time a memory address is executed flip the bit

* Difficulties implementing CDL are:

    * Many games using different access to same data. For example read long to read two words (for example coordinates x, y). [2]

#### Bizhawk CDL Tool

Since Bizhawk is fully open source we can inspect how the CDL was implemented for this multi-emulator system.

#### CDL.cs (Showing cdl statistics window)

CDL.cs contains the functionality for interacting with the CodeDataLogger window seen in the screenshot below:

![image alt text]({{ site.url }}/public/IiA83YXfAzYaSGTnQsabPA_img_2.png)

The list is made up of a number of columns showing the statistics collected in the CDL:

<table>
  <tr>
    <td>Name</td>
    <td>Displayed Information</td>
  </tr>
  <tr>
    <td>CDL File @</td>
    <td>Address of the block in the cdl file</td>
  </tr>
  <tr>
    <td>Domain</td>
    <td>Name of the block</td>
  </tr>
  <tr>
    <td>%</td>
    <td>Percentage of the block that has been mapped (accessed in some way either as code or data)</td>
  </tr>
  <tr>
    <td>Mapped</td>
    <td>Number of mapped bytes</td>
  </tr>
  <tr>
    <td>Size</td>
    <td>Total number of bytes in the block</td>
  </tr>
  <tr>
    <td>0x01.. 0x80</td>
    <td>Percentage or Number of bytes accessed as...
0x01: 
0x02:
0x04:
0x08
0x10:
0x20:
0x80:</td>
  </tr>
</table>


#### Calculating Statistics

In order to calculate the statistics shown in the list bizhawk has the following logic:

* First loop over every byte in the block and for each byte:

    * Count the number of times this byte value exists

    * Since each byte can only have a value between 0 -> 255, you just need a map with size 256 that contains the count for each possible byte value.

* Next, now that we have the count of each byte value we need to find out the count for each bit being set to 1

    * Create a new array with length 8 of the totals for each bit being set to 1, where each element is the count of that bit being set.

    * So for each possible byte value (0 -> 255) use bitwise arithmetic to find out if the first bit is set

    * If the first bit is set then add the number of times this byte appeared to the totals array for this bit

        * To check if the first bit is set: (byteValue & 0x01) != 0

        * To check if the last bit is set: (byteValue & 0x80) != 0

#### CodeDataLog.cs (.cdl file read/write)

The CodeDataLog class contains logic for saving and importing CDL files.

* The **SaveInternal** method on this class is what actually writes the cdl data to a file on disk

    * ![image alt text]({{ site.url }}/public/IiA83YXfAzYaSGTnQsabPA_img_3.png)

    * It uses the class as a Key Value Pair (kvp) where the key is the block name (e.g Cartridge ROM, WRAM etc)

    * The value is the byte array of this block and before its written to the file the length of the block is written so it can be easily parsed when read.

* The Load method on this class is what actually reads in the cdl data from a cdl file.

This includes opening and saving a cdl file and displaying the statistics in the list view.

[View Source for CDL.cs](https://github.com/TASVideos/BizHawk/blob/15a25bdd8763b3526b25e73406557cbb2305d2b0/BizHawk.Client.EmuHawk/tools/CDL.cs) 

#### Gameboy (Gambatte in Bizhawk)

* [https://github.com/TASVideos/BizHawk/blob/15a25bdd8763b3526b25e73406557cbb2305d2b0/BizHawk.Emulation.Cores/Consoles/Nintendo/Gameboy/Gambatte.ICodeDataLog.cs](https://github.com/TASVideos/BizHawk/blob/15a25bdd8763b3526b25e73406557cbb2305d2b0/BizHawk.Emulation.Cores/Consoles/Nintendo/Gameboy/Gambatte.ICodeDataLog.cs) (public partial class Gameboy : ICodeDataLogger) Only useful as an entry point

## References

1. **[Tomaitheous - details about format of CD**L](http://gendev.spritesmind.net/forum/memberlist.php?mode=viewprofile&u=83&sid=e08651c26032bd6aed6ed20888315ea5) and implementation details

2. **[r57shel**l](http://gendev.spritesmind.net/forum/memberlist.php?mode=viewprofile&u=609&sid=e08651c26032bd6aed6ed20888315ea5) - difficulties of implementing CDL

3. [http://www.fceux.com/web/help/fceux.html?CodeDataLogger.html](http://www.fceux.com/web/help/fceux.html?CodeDataLogger.html) 

