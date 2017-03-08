---
layout: post
title: "Loop Wisely in Java"
description: ""
category:
tags: []
---
{% include JB/setup %}

The following list is from the google I/O talk in 2008 called "Dalvik Virtual Machine Internals" its a list of ways to loop over a set of objects in order from most to least efficient:

(1) `for (int i = initializer; i >=0; i--) //hard to loop backwards`
(2) `int limit = calculate_limit(); for (int i= 0; i< limit; i++)`
(3)` Type[] array = get_array(); for (Type obj : array)`
(4) `for (int i =0; i< array.length; i++) //gets array.length everytime`
(5) `for (int i=0; i < this.var; i++) //has to calculate what this.var is`
(6) `for (int i=0; i < obj.size(); i++) //even worse calls function  each time`
(7) `Iterable list = get_list(); for (Type obj : list) //generic object based iterators slow!`

The first 3 are in the same territory of efficiency, avoid 7 if possible.

This is mainly advice to help battery life but could potentially help Java SE code too.

Another piece of advice he gives is to avoid memory allocation as much as possible, especially in loops!
