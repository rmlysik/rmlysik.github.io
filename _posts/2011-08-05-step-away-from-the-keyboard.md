---
layout: post
status: publish
published: true
title: Step Away from the Keyboard
date: '2011-08-05 03:27:41 -0400'
date_gmt: '2011-08-05 03:27:41 -0400'
categories:
- Uncategorized
tags: []
comments: []
---
It's tempting to begin a project like this by hammering away at the keyboard writing code. The gratification is immediate, you can see results and feel some sense of accomplishment. This is also a good way to generate unmaintainable and fragile code. The other extreme, however, can be just as bad, that is: excessive analysis to the point where nothing ever gets built. What I intend to do is define preliminary requirements for this application that will serve as a road map for development. Without this how will we know if we're on the right track?

With software, unlike building a bridge, the expense of throwing away something you've built consists only of the time you've invested. There has been no blasting with explosives, no excavation, no pouring of concrete footings only to find that you're off by a yard.

As we're building this system, wouldn't it also be nice to be able to verify that it meets the requirements we've set? Otherwise, what is the point of requirements? Whether I'm the developer, tester or customer this is critical. Ideally the test cases should map to our requirements and we have an outline for how we'd test the application to verify that the requirements have been met.

Game Mechanics
--------------

When a new game is started, an introductory message is displayed to the player which includes a list of supported commands.

A summary of the player's initial location is also displayed that is equivalent to the information displayed as a result of entering the "look" command.
Game play consists of text based command and response dialog. For example, to move from one location to another within the game, the player might enter the command "go north".
A game ends when the player enters the command "quit" or when the player's score has reached the maximum score for the game.

Commands
--------

### Look

The "look", or shorthand version "l", command displays information about the player's current location such as the location name, a brief description, available exits and all visible items. For example:

**Dining Room**

You're in the dining room

Obvious exits: East, North

You can also see: Golden Chalice

### Go

The "go" command is used in conjunction with a direction to move from one location to another. For example "go north", or simply "north", will result in changing the player's location to the location that is defined as being "north" of the player's original location. The player may also use shorthand expressions for navigation: "n" for "north", "u" for "up", etc. Valid directions are "north", "south", "east", "west", "up", and "down" and their shorthand equivalents: "n", "s", "e", "w", "u" and "d". When the player enters a navigation command, a summary of the new location is displayed equivalent to the result of having entered the "look" command.

If the player attempts to go in a direction that is not available, the message "You can't go that way" will be displayed. This message will also be displayed if the user enters an invalid direction. Not all directions will be available exits. Available exits for each location must be configurable, i.e. it must be possible to assign a direction and its destination to each location.

### Inventory

The "inventory", or shorthand version "i", command displays a list of the items the player is currently carrying, for example "You're carrying: Golden Chalice". If the player has no items in their inventory the message "You're carrying nothing" is displayed.

### Take

The "take" command is used in conjunction with the name of an item. If the item is present in player's current location then the item is added to the player's inventory, removed from the available items in the room, and the message "Taken" is displayed to the player. If the item does not exist in the player's current location then the message "You can't see any such thing" is displayed. If the item exists in the player's inventory then the message "You're already carrying that" is displayed.

### Drop

The "drop" command is used in conjunction with an item name, as in "drop candelabra". If the item is present in the player's inventory then the item is removed from their inventory and added to the items in the player's current location and the message "Dropped" is displayed to the player. If the item does not exist in the player's inventory then the message "You can't see any such thing" is displayed to the player.

### Help

The "help", or shorthand "h", command displays a short message which includes the list of available commands. A help message specific to the location that the player is in may also be appended to the message.

### Score

The "score" command displays the player's current score and maximum achievable score for the game. For example, "You have X of a possible Y
points" where X is the player's score, and Y is the maximum achievable score.

I'm leaving requirements regarding custom commands and scoring for the next phase. At this point I believe we have enough to get started.
To test the functionality of the system I'll create the fictional game, Haunted Mansion. I'll elaborate on this game as we move forward in order to add more features and test cases. For now, here's what we have:

![Haunted Mansion - First Floor](/images/posts/2011/08/Haunted-Mansion-First-Floor.jpg "Haunted Mansion - First Floor")

![Haunted Mansion - Second Floor](/images/posts/2011/08/Haunted-Mansion-Second-Floor.jpg "Haunted Mansion - Second Floor")

The player will start in the foyer, will have an initial score of zero and will have no items in their inventory.

Next step: Design...
