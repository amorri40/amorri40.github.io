---
layout: post
title: "Clang Plugin Xcode headaches"
description: ""
category:
tags: []
---
{% include JB/setup %}


Recently I have been writing a plugin for the Clang C/C++ compiler in order to generate code just before compile time.

This has been going fairly smoothly until I decided to create an Xcode project to allow easier breakpoint debugging with gdb.

Setting up the compiler flags was fairly straightforward, the main problems came from the linking stage.

Using the exact same linking flags as the working build script Xcode kept complaining about undefined functions such as "raw_fd_ostream" in the llvm library.


It turns out that there is an easy fix but it wasn't clear where to look. For anyone else experiencing the same issue make sure to set the standard library settings in XCode to "Compiler Default" like so:<br>

<a href="http://2.bp.blogspot.com/--8muxSX_JoI/Ubthv3HIJPI/AAAAAAAAAC4/iw5ms_zhOJE/s1600/Screen+Shot+2013-06-14+at+19.26.42.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="192" width="640" src="http://2.bp.blogspot.com/--8muxSX_JoI/Ubthv3HIJPI/AAAAAAAAAC4/iw5ms_zhOJE/s640/Screen+Shot+2013-06-14+at+19.26.42.png" class="" style="display: inline-block;"></a>




This will allow any clang plugins you are developing to compile and link succesfully :)

It is such a simple solution now but I was so sure that it was a problem in the internals of my LLVM build process that I managed to spend a whole morning getting very frustrated modifying the LLVM libraries when all I needed to do was Change those compiler settings!!