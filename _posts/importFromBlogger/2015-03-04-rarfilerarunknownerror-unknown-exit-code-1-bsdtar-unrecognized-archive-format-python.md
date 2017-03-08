---
layout: post
title: "rarfile.RarUnknownError: Unknown exit code [1]: bsdtar: Unrecognized archive format Python"
description: ""
category:
tags: []
---
{% include JB/setup %}

So recently I have been trying to unrar files in python with limited success.

After spending what felt like hours trying to track down the problem it was quite a simple fix.

So if you get this error:
``rarfile.RarUnknownError: Unknown exit code [1]: bsdtar: Unrecognized archive format``

Then you just need to install the unrar executable like so:
# On Mac:
`brew install unrar`
# On Ubuntu:
`apt-get install unrar`

Good luck!
