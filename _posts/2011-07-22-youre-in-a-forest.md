---
title: You're in a Forest
date: '2011-07-22 02:50:36 -0400'
date_gmt: '2011-07-22 02:50:36 -0400'
categories:
- Uncategorized
tags: []
comments: []
---
Thus begins the classic text adventure game [Adventureland](https://en.wikipedia.org/wiki/Adventureland_(video_game) "Adventureland"){:target="_blank"} by Scott Adams. If you're unfamiliar with text adventures I don't blame you. Text adventures were popular at a time when graphics and sound for personal computers were limited and so we were left with games which required that we use our imagination (how absurd!). Gameplay would typically involve the display of a short description of the players current location, as well as exits and items that are present (and which might be useful). A prompt is displayed at which the player may enter a one or two word sentence, such as *go up*, or simply *up*. An example from the aforementioned game, Adventureland, follows:

**Forest**

You're in a forest.

Obvious exits: North, South, East, West, Up.

You can also see: trees.

    > up

**Branch**

You're in a branch on the top of an old oak tree.

To the east you see a meadow beyond a lake.

Obvious exits: Down.

    > down

**Forest**

You're in a forest.

Obvious exits: North, South, East, West, Up.

You can also see: trees.

    > east

**Meadow**

You're in a sunny meadow.

Obvious exits: North, South, East, West.

You can also see: sleeping Dragon - sign reads- IN SOME CASES MUD IS GOOD, IN OTHERS...

    >

If you'd like, you can play an on-line version of the original game [here](http://www.freearcade.com/Zplet.jav/Advland.html "Adventureland game"){:target="_blank"}.
So why do I bring this up? Part of it is me reminiscing about my misspent youth, but I also thought this would be a fun exercise for developing an application from the ground up. This is also a rather well understood problem, having its earliest incarnation back in 1975 with [Adventure](https://en.wikipedia.org/wiki/Interactive_fiction#History "Adventure"){:target="_blank"} written by Will Crowther in Fortran on the PDP-10.

In doing research on this topic I also came across a more recent incarnation of this gaming genre at [textadventures.co.uk](http://textadventures.co.uk/ "TextAdventures"){:target="_blank"}. This website allows you to browse for games by categories such as educational, fantasy, mystery, etc. You can start playing a game right within the browser, or you can download a game and play offline. They also provide a tool named Quest that you can download and use to create your own text adventures.

In the posts that follow I will delve further into developing a text adventure platform inspired by the work of Scott Adams and Will Crowther. I hope to use this exercise as a way to explore the software development process and to perhaps learn a few things along the way.
