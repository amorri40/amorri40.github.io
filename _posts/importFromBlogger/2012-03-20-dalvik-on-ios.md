---
layout: post
title: "Dalvik on iOS"
description: ""
category: iOS
tags: [Android]
---
{% include JB/setup %}

Recently I came across the in-the-box project which aims to run the dalvik virtual machine (which is the java VM for android) on iOS devices.

They have a video showing a basic hello world example running in the dalvik vm on ios:
[http://www.youtube.com/watch?v=fhyd18h_as4](http://www.youtube.com/watch?v=fhyd18h_as4)

The code is available on googlecode:
[http://code.google.com/p/in-the-box/](http://code.google.com/p/in-the-box/)

The xcodeproject builds without problems and runs in the simulator, I haven't tested on the actual device as my apple developer license expired a few months ago.

It is tempting to write an app in java and see if it passes the apple terms, they may have relaxed their policy on interpreted code but some apps are still rejected that execute bytecode in this manner.

I'm also not sure if dalvik uses executable memory which is definitely banned (only safari is allowed to for its javascript implementation).

Dalvik also seems like a good candidate for a very efficient scripting language for games, it is designed to run on devices with a very minimal RAM requirement and the .dex format is optimised to save space.

For more details on the benefits and optimisations of dalvik there is this very interesting google talk:
[http://www.youtube.com/watch?v=ptjedOZEXPM](http://www.youtube.com/watch?v=ptjedOZEXPM)

I have been testing out the main Java API functionality and it seems to be fully functional, only started testing the Android api, at the moment I am figuring out how to implement the GUI parts of the library to be able to hopefully show some android components and eventually run a full android app on iOS and possible Mac.

First you will need to convert the android libraries to normall java class jar files, you can do this with a tool called dex2jar:
[http://code.google.com/p/dex2jar/downloads/list](http://code.google.com/p/dex2jar/downloads/list)

After downloading find your "/in-the-box/InTheBoxSim/framework/" folder and for each jar file, extract it with a zip tool and run the following command on the classes.dex located in that jar file.
Just run `sh dex2jar.sh classes.dex` to get the output jar files in normal java class format.

To compile java for testing in this iOS version of dalvik you need to pass the relevant android libraries to the javac command like so:
```bash
javac Hello.java -classpath /in-the-box/InTheBoxSim/framework/framework/framework.jar:/in-the-box/InTheBoxSim/framework/core/core.jar
```

After creating a java jar file with all the classes you want we will need to convert it to the dex format to run it on dalvik.

To convert a normal jar of java classes (compiled with javac) to the dex format you can use:
```bash
dx --dex --output=DalvikClasses.jar normalClasses.jar
```
Now just Move DalvikClasses into the bundles resources in the xcodeproject and update the "InTheBoxSim/Supporting Files/main.m" to the normalClasses.jar and the main class you want to run!

Currently i'm modifying the in-the-box files to get the android GUI somewhat working, i'll create an update blog post when I make some significant progress.