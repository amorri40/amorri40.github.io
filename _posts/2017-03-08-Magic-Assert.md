---
title: Magic Assert
layout: post
author: amorri40
permalink: /magic-assert/
tags:
- javascript
- testing
source-id: 1LJapSC7xZeZbOmbuUkk2zi0IPXYRCOL5WXQhpPGg9Fo
published: true
---
Magic Assert

The test framework Ava has introduced a very useful new feature that they call "Magic Assert". 

It is basically a normal assert statement, but when the result is not expected it shows a nice diff explaining what it go and what it was expecting. 

## Screenshot of Ava Magic Assert

This is the main feature that pulls me towards using Ava instead of Mocha or Jest testing frameworks. However it got me wondering, why not have an assert library that is generic enough to work with all test runners. Similar to how Chai works seamlessly across these frameworks it would be great to have a "magic-assert" library that also works with the testing framework of your choice.

Watch this space! 😉

