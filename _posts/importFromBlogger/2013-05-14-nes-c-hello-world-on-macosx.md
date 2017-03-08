---
layout: post
title: "NES C Hello World on MacOSX"
description: ""
category: [Retro,CProgramming]
tags: []
---
{% include JB/setup %}

<div class="article-content entry-content" itemprop="articleBody">Recently I have become interested in assembly language and romhacking in general, so I thought I would try implementing a simple hello world program in CC65. I'm not intending on writing NES game in C but rather using C as a basis to try and learn assembly language programming on the&nbsp;6502 processor.<br>
<br>
First download the CC65 source files from:<br>
ftp://ftp.musoftware.de/pub/uz/cc65/snapshot/<br>
<br>
Next open a terminal in the directory and type:<br>
make -f make/gcc.mak<br>
<br>
Wait until that has finished and type:<br>
sudo make -f make/gcc.mak install<br>
<br>
Now lets make sure it has installed correctly:<br>
which cc65<br>
<br>
That should print:<br>
/usr/local/bin/cc65<br>
<br>
now create a new folder called hello_world wherever you want your project to be located:<br>
mkdir hello_world<br>
<br>
Move the include and lib folders from the source into that new directory, if you are missing the lib folder you need to download the nes library from the same ftp link you obtained cc65.<br>
<br>
Create a new .c file called hello_world.c, for the contents I used the c code from this tutorial:<br>
http://rpgmaker.net/tutorials/227/<br>
<br>
<blockquote class="tr_bq">
<blockquote class="tr_bq">
/*</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; Hello, NES!</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; writes "Hello, NES!" to the screen</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; written by WolfCoder (2010)</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
*/</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
/* Includes */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
#include <nes .h=""></nes></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
/* Writes the string to the screen */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
/* Note how the NES hardware itself automatically moves the position we write to the screen */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
void write_string(char *str)</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
{</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* Position the cursor */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* We only need to do this once */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* This is actually 2 cells down since the first 8 pixels from the top of the screen is hidden */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2006) = 0x20;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2006) = 0x41;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* Write the string */</blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; while(*str)</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; {</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; &nbsp; &nbsp; /* Write a letter */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; &nbsp; &nbsp; /* The compiler put a set of graphics that match ASCII */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; &nbsp; &nbsp; *((unsigned char*)0x2007) = *str;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; &nbsp; &nbsp; /* Advance pointer that reads from the string */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; &nbsp; &nbsp; str++;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; }</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
}</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
/* Program entry */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
int main()</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
{</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* We have to wait for VBLANK or we can't even use the PPU */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; waitvblank(); /* This is found in nes.h */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* This is a really strange way to set colors, don't you think? */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* First, we need to set the background color */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2006) = 0x3F;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2006) = 0x00;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2007) = 1;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* Then, we need to set the text color */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2006) = 0x3F;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2006) = 0x03;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2007) = 0x30;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* We must write our message to the screen */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; write_string("Hello, NES!");</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* Set the screen position */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* First value written sets the X offset and the second is the Y offset */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2005) = 0x00;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2005) = 0x00;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* Enable the screen */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* By default, the screen and sprites were off */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; *((unsigned char*)0x2001) = 8;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* Wait */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; /* The compiler seems to loop the main function over and over, so we need to hold it here */</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; while(1);</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp;&nbsp;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
&nbsp; &nbsp; return 0;</blockquote>
<blockquote class="tr_bq">
<br></blockquote>
<blockquote class="tr_bq">
}</blockquote>
</blockquote>
<br>
Compile the hello_world.c to a nes rom like so:<br>
cl65 -L .\lib -t nes -I .\include hello_world.c -o hello_world.nes<br>
<br>
Download and install a mac nes emulator such as nestopia to test your new hello world rom!<br>
<br>
If all went well it should show something like this:<br>
<div class="separator" style="clear: both; text-align: center;">
<a href="http://2.bp.blogspot.com/-WvP-yRGfhp4/UZI0rlwb35I/AAAAAAAAACk/c2VoYE1K1pM/s1600/Screen+Shot+2013-05-14+at+13.56.25.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-WvP-yRGfhp4/UZI0rlwb35I/AAAAAAAAACk/c2VoYE1K1pM/s1600/Screen+Shot+2013-05-14+at+13.56.25.png" class="" style="display: inline-block;"></a></div>
<br>
<br>
Thanks to:<br>
mrsid from lemon64.com for compiling instructions<br>
WolfCoder from rpgmaker.net for hello world code and tutorial</div>