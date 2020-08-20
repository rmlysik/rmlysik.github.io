---
title: An Initial Game Design
date: '2011-08-06 16:58:51 -0400'
date_gmt: '2011-08-06 16:58:51 -0400'
categories:
- Uncategorized
tags: []
comments: []
---
Based on analysis of the text adventure game, and using the requirements described in my previous post, I've come up with my initial stab at an object-oriented design for this problem. I've broken down the responsibilities into four main classes: Game, Item, Location and Player.

Using [UML](https://en.wikipedia.org/wiki/Class_diagram "UML Class Diagram"){:target="_blank"} notation this appears as:

![Class Diagram](/images/posts/2011/08/Class-Diagram2.jpg "Class Diagram")

Game
----

This is the class that does the brunt of the work and is responsible for processing commands, handling player movement and managing player inventory and scoring. The protected methods drop, go, help, inventory, look, score and take handle the respective commands sent by the player. The main public methods are create, which creates an instance of the game, and process command, which takes a command entered by the player and interprets it to determine what, if any, action should be taken.

### Properties

**locations**

An array of Item objects that are available within the game.

**items**

An array of Item objects that are used in the game.

**player**

An instance of a Player object, used to track player's location and inventory

### Methods

**create**

Takes an XML string as an argument and populates the initial game attributes.

**processCommand**

Takes a string as an argument and performs the specified action. For example, command "go north" will move the player to the location north of their current location. The command string may consist of a single word, such as "help", or a combination of words such as "take candelabra". If the command is not supported, the message "That's not a verb I recognize" is returned to the player. Otherwise, the corresponding method, detailed below, is called.

**drop**

Takes an item name as an argument. If the item exists in the player's inventory then the item is removed from their inventory, added to the items array of the current location, and the message "Dropped" is returned to the player. Otherwise the message "You can't see any such thing" is returned to the player.

**go**

Takes a direction as an argument and returns an instance of a Location corresponding to that direction, or null if not found. The new location is determined using the direction as a look-up key into the exits array of the player's current location. If there are no exits in the requested direction, the message "You can't go that way" is returned to the user. Otherwise, the player's current location is changed to the new location, and a summary of the location (equivalent to the result of the "look" command) is returned to the player.

**help**

Returns a message to the player indicating all available commands. The hint property of the player's current location is also appended to the message that is returned to the player.

**inventory**

Returns a message to the player listing the items currently in their inventory. If the player is not carrying any items, the message "You're carrying nothing" is returned to the player. Otherwise the message "You're carrying", followed by a list of the items in the player's inventory is returned.

**look**

Returns a summary of the current location to the player, including location name, description, available exits and items found at this location.

**score**

Returns a message to the player indicating their current points out the total available points.

**take**

Takes the name of an item as an argument and adds the item to the player's inventory. If the item doesn't exist at the current location, the message "You can't see any such thing" is returned to the player. Otherwise, the item is added to the player's inventory and the message "Taken" is returned to the player.

Item
----

The Item class represents an object in the game, like a chalice or candelabra. Items can be moved from one location to another or they may be placed in the players inventory. There are no methods defined at this point, although we'll revisit this later when custom actions are implemented.

### Properties

**name**

The name of the item, e.g. "Golden Chalice"

**description**

A short description of the item, e.g. "An elaborately decorated gold chalice."

Location
--------

The Location class represents a place in the game, such as the foyer, or dining room, in our example game. A location has a name and a description and may have items and exits as well.

### Properties

**name**

The name of the location, e.g. "Dining Room"

**description**

A short description of the location, e.g. "You are in the dining room."

**hint**

A message that will be displayed to the player when they enter the "help" command at this location. May be left blank.

**items**

An array of Item objects found at the location.

**exits**

An array of Locations whose keys are the compass directions and up / down representing available exits from the location.

### Methods

**hasItem**

Takes the name of the string as an argument and returns true if the item exists in this location, otherwise it returns false.

**addItem**

Adds an Item instance to the location item array.

**removeItem**

Removes an item from the location item array.

**hasExit**

Takes a direction, e.g. North, South, etc. as an argument and returns true if the location has an exit for that direction.

**getExitLocation**

Takes a direction as an argument and returns an instance of a Location corresponding to that direction, or null if not found.

Player
------

The Player class manages the player's location and inventory of items.

### Properties

**currentLocation**

The location of the player in the game, an instance of a Location.

**inventory**

An array of Item objects in the player's possession.

### Methods

**hasItem**

Checks player's inventory to determine whether item exists, returns true if found otherwise returns false.

**addItem**

Adds an item to the player's inventory.

**removeItem**

removes an item from the player's inventory.

**moveToLocation**

Sets the player's currentLocation to the location specified.

It should now be fairly straightforward to implement this design in code. The nice thing is that the descriptions can also be carried directly over as comments within the code.

Next stop...Implementation!
