---
title: Bitwise Operators (for Emulation)
layout: post
author: amorri40
permalink: /bitwise-operators/
tags:
- nintendo
- gameboy
- emulation
source-id: 1wAhKgLnD6sizvWUYdisZrtZRa80FnjXgKfMALXVgXVc
published: true
---
Bitwise Operators

All these operators work on the BITS of the data, hence why they are called Bitwise operators.

Key:

<table>
  <tr>
    <td>Bit number</td>
  </tr>
  <tr>
    <td>Value when Bit is Set to 1 (divide by this number if you want a right shift)</td>
  </tr>
  <tr>
    <td>Hex Value</td>
  </tr>
</table>


<table>
  <tr>
    <td>0</td>
    <td>1</td>
    <td>2</td>
    <td>3</td>
    <td>4</td>
    <td>5</td>
    <td>6</td>
    <td>7</td>
    <td>8</td>
    <td>9</td>
    <td>10</td>
    <td>11</td>
    <td>12</td>
    <td>13</td>
    <td>14</td>
    <td>15</td>
  </tr>
  <tr>
    <td>1</td>
    <td>2</td>
    <td>4</td>
    <td>8</td>
    <td>16</td>
    <td>32</td>
    <td>64</td>
    <td>128</td>
    <td>256</td>
    <td>512</td>
    <td>1024</td>
    <td>2048</td>
    <td>4096</td>
    <td>8192</td>
    <td>16384</td>
    <td>32768</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td></td>
    <td>0x400</td>
    <td>0x800</td>
    <td>0x1000</td>
    <td>0x2000</td>
    <td>0x4000</td>
    <td>0x8000</td>
  </tr>
</table>


## Right Shift Operator (>>)

Example:

You are making the number smaller basically by dividing it by 2 for each bit you want to move right.

So to get the value just divide the number by 2 to the power of the bit number.

You can use the table above to find out what to divide by based on the bits that you want shifted. For example if you do a bit shift of 12 (>> 12) you divide the number by 4096

<table>
  <tr>
    <td>const numberYouWantBitShifted = 254; // binary: 11111110
numberYouWantBitShifted >> 1 === 127;
numberYouWantBitShifted >> 2 === 63;
numberYouWantBitShifted >> 3 === 31; // ((254/2)/2)/2




const result =  numberYouWantBitShifted >> HowManyBitsToRemoveToTheRight;</td>
  </tr>
</table>


The right-shift operator causes the bit pattern in shift-expression to be shifted to the right by the number of positions specified by additive-expression. For unsigned numbers, the bit positions that have been vacated by the shift operation are zero-filled. For signed numbers, the sign bit is used to fill the vacated bit positions. In other words, if the number is positive, 0 is used, and if the number is negative, 1 is used.

Gambatte emulator example

## Bitwise AND (&)

The bitwise AND operator returns a number where each bit is 1 only if both numbers bits were 1 otherwise it makes the bit 0.

### Example: Value & 0x7F

You can use the bitwise And operator with 0x7F to remove the most significant bit!

It also ensures that the number is positive (sign bit) [1]

This works because:

*  0x7f is 0111 1111

   [ ](https://stackoverflow.com/questions/15394454/bitwise-logic-what-does-anding-something-with-0x7f-accomplish)

Also (P & 0x7F) has the same effect as basically subtracting 0xFF00 from the Pointer address

### Example: Value & 0x80

This checks if the 8th bit in a byte value is set to 1, useful if the byte value is a bit set containing a flag for each bit.

This is also useful for checking if the value is greater than 128, if it is then the resulting value will be 128 otherwise 0.

* 0x80 is 1000 0000 (128 bit is set only)

E.g in gambatte video.cpp: 

<table>
  <tr>
    <td>!(ppu.lcdc() & 0x80) // make sure the lcd enable bit is set to 0</td>
  </tr>
</table>


References

1. [https://stackoverflow.com/questions/15394454/bitwise-logic-what-does-anding-something-with-0x7f-accomplish](https://stackoverflow.com/questions/15394454/bitwise-logic-what-does-anding-something-with-0x7f-accomplish) 

