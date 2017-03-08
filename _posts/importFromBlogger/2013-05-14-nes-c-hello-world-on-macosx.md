---
layout: post
title: "NES C Hello World on MacOSX"
description: ""
category: [Retro,CProgramming]
tags: []
---
{% include JB/setup %}

Recently I have become interested in assembly language and romhacking in general, so I thought I would try implementing a simple hello world program in CC65. I'm not intending on writing NES game in C but rather using C as a basis to try and learn assembly language programming on the&nbsp;6502 processor.

First download the CC65 source files from:
[ftp://ftp.musoftware.de/pub/uz/cc65/snapshot/](ftp://ftp.musoftware.de/pub/uz/cc65/snapshot/)

Next open a terminal in the directory and type:
```make -f make/gcc.mak```

Wait until that has finished and type:
```bash
sudo make -f make/gcc.mak install
```

Now lets make sure it has installed correctly:
```which cc65```

That should print:
```/usr/local/bin/cc65 ```

now create a new folder called hello_world wherever you want your project to be located:
mkdir hello_world

Move the include and lib folders from the source into that new directory, if you are missing the lib folder you need to download the nes library from the same ftp link you obtained cc65.

Create a new .c file called hello_world.c, for the contents I used the c code from this tutorial:
http://rpgmaker.net/tutorials/227/

```C
/*

	Hello, NES!

	writes "Hello, NES!" to the screen



	written by WolfCoder (2010)

*/



/* Includes */

#include <nes.h>



/* Writes the string to the screen */

/* Note how the NES hardware itself automatically moves the position we write to the screen */

void write_string(char *str)

{

	/* Position the cursor */

	/* We only need to do this once */

	/* This is actually 2 cells down since the first 8 pixels from the top of the screen is hidden */

	*((unsigned char*)0x2006) = 0x20;

	*((unsigned char*)0x2006) = 0x41;

	/* Write the string */

	while(*str)

	{

		/* Write a letter */

		/* The compiler put a set of graphics that match ASCII */

		*((unsigned char*)0x2007) = *str;

		/* Advance pointer that reads from the string */

		str++;

	}

}



/* Program entry */

int main()

{

	/* We have to wait for VBLANK or we can't even use the PPU */

	waitvblank(); /* This is found in nes.h */



	/* This is a really strange way to set colors, don't you think? */

	/* First, we need to set the background color */

	*((unsigned char*)0x2006) = 0x3F;

	*((unsigned char*)0x2006) = 0x00;

	*((unsigned char*)0x2007) = 1;

	/* Then, we need to set the text color */

	*((unsigned char*)0x2006) = 0x3F;

	*((unsigned char*)0x2006) = 0x03;

	*((unsigned char*)0x2007) = 0x30;



	/* We must write our message to the screen */

	write_string("Hello, NES!");



	/* Set the screen position */

	/* First value written sets the X offset and the second is the Y offset */

	*((unsigned char*)0x2005) = 0x00;

	*((unsigned char*)0x2005) = 0x00;



	/* Enable the screen */

	/* By default, the screen and sprites were off */

	*((unsigned char*)0x2001) = 8;



	/* Wait */

	/* The compiler seems to loop the main function over and over, so we need to hold it here */

	while(1);



	return 0;
}
```

Compile the hello_world.c to a nes rom like so:
```bash
cl65 -L .\lib -t nes -I .\include hello_world.c -o hello_world.nes
```
Download and install a mac nes emulator such as nestopia to test your new hello world rom!

If all went well it should show something like this:
<div class="separator" style="clear: both; text-align: center;">
<a href="http://2.bp.blogspot.com/-WvP-yRGfhp4/UZI0rlwb35I/AAAAAAAAACk/c2VoYE1K1pM/s1600/Screen+Shot+2013-05-14+at+13.56.25.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" src="http://2.bp.blogspot.com/-WvP-yRGfhp4/UZI0rlwb35I/AAAAAAAAACk/c2VoYE1K1pM/s1600/Screen+Shot+2013-05-14+at+13.56.25.png" class="" style="display: inline-block;"></a></div>


Thanks to:
mrsid from lemon64.com for compiling instructions
WolfCoder from rpgmaker.net for hello world code and tutorial