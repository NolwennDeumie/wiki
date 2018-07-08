---
title: "Onglet Tileset"
description: "Documentation de l'onglet Tilesets pour RPG Maker VX Ace et MV."
og_image: "/assets/default_opengraph.png"
---


What are Maps?

Maps are the data that represent the setting for your game. Maps will unfold based on where a character moves on the map when playing the game.

A map's design is edited by placing together parts using for composing your map called "Tiles".
Map Basic Specifications
Role of Tiles

Tiles are images which give a map its appearance, and are configured to allow or not allow a character to move across that tile.

In one map, multiple tiles grouped together assigned to be one piece of data are called a "Tileset", which is used as the basis of designing the shape of a map. You can instantly change the appearance of a map by changing the tileset you are using. The contents of a tileset can be edited using the [Database].
Tile Classifications

It is possible to include 5 types of tiles for A through E in one tileset. A is the lower layer which represents the terrain and ground, and B through E are upper layer tiles which represent surface elements such as trees and bushes or sign boards.

It is possible to place an upper layer and lower layer tile on the same location on the map. By using this two-layer composition, it is possible to create a very detailed and intricate map.

As a standard, tiles that represent things such as the ocean, grasslands, floors and walls are the lower layer tiles, and upper layer tiles used to decorate those layers are provided.
Moreover, it is now possible to overlap two types of upper layer tiles allowing for more variation in this version.


Other Editing Functions

Autotile
    A feature called [Autotile] is included in the tiles displayed in the A tab of the Tile Palette. With autotiles, one type of tile contains several patterns, and the border of the tile will be adjusted automatically depending on how the tiles are placed. Tiles which have the autotile function are assigned to [A1] through [A4] in the database [Tilesets].

    Moreover, you can temporarily disable the autotile function by holding [Shift] and drawing tiles or using the eyedropper. 
Autoshadows
    Within autotiles, by placing two or more tiles vertically, a shadow will automatically be drawn to the bottom right of that tile. However, specified tiles will not have shadows drawn on them.
Shadow Pen
    The Shadow Pen is a tool that allows you to draw shadows for walls and buildings. You can darken the hue by 1/4th of the size of a tile.

    Click the [Shadow Pen] button on the toolbar (or go to [Draw] → [Shadow Pen] in the menu), and click on the Map View. A shadow is drawn by clicking on a part which has no shadow, and by clicking a part which already has a shadow, that shadow will be removed.
Upper Layer Tile Special Specifications

        You can layer 2 different types on the upper maps B-E.
        * When layering a 3rd tile, the 1st upper tile will disappear.
        * When the 3rd tile layered is the same as the 2nd tile, the first tile will not disappear.
        * Only the upper left B tile can erase all upper tiles.
        When a passable tile and an impassable tile are layered, the effect of the tile layered last takes priority.
        * Even when a passable ☆ tile is on the bottom, the tile with the ☆ will be displayed on top.
        * When a passable ☆ tile is layered, the impassable tile's effect will take priority.

Lower Layer Tile Special Specifications
    Amongst the tiles that are displayed in the [A] tab of the Tile Palette, those items found in [A2] in the tileset properties are divided into [Base] (tiles 1 to 4 from the left, or the left half) and [Decoration] tiles (tiles 5 to 8 from the left, or the right half). Decoration tiles can be placed on top of base tiles.

    However, for those [Tilesets] which have their [Mode] set to [World Type] in the tileset properties, when placing a decoration tile that is stacked on a 2nd or 4th base tile, the base tile will change either the 1st or 3rd base tile. 

Tileset Settings

    RPG Maker MV > Database > Tileset Settings 

Role of Data

Tilesets are the collection of "Tiles" used to design your map. Create tiles by setting whether a character can walk on the image used for the tile, and also the behavior in the game.

Original images created for the map can be used as well by creating tilesets which use those images, and assign as map data.

Moreover, whether or not vehicles (boats/large ships) can go over tiles is determined by the position over the tileset. For more information, please view Asset Standards.
Planes are able to travel over all tiles. However, there are only able to land on tiles which can be walked on.
Parameter Details
General Settings
Name

A tileset's name. This property is just used in the editor (does not affect the game).
Mode

The purpose of the tileset. This primarily influences the treatment of special specifications of lower tiles and battlebacks.
Basically, choose [Field Type] for tiles which represent the overworld like the ocean and land, and [Area Type] for all other situations.

Images

Settings for images used for tiles. Specify the file you want to use for each type (Sets A through E) in the [Select an Image] window that is displayed when you press the button for each type. An image's contents will be displayed in the [Tile List] on the right.
Tile List

The image used for a tileset in [Images] will be displayed. You can switch the images displayed by clicking tabs [A] through [E] at the bottom. The tiles for the images specified in [A1] through [A5] in the [Images] section will be displayed in order.

Marks representing the parameter values in the current settings editing mode will be displayed on top of each tile. You can change these parameter values by clicking the tile.
Passage

Switch to the editing mode where you can set whether a tile can be entered or not. Tiles marked with a [○] can be entered, ones marked with an [×] cannot be entered. Those which have a [☆] can also be entered, however this is for when hiding characters behind buildings (only possible in all other tabs except [A]).
Passage (4 dir)

Switch to the editing mode where you can set the direction from where tile can be entered. Use [Passage: Block] when creating tiles that can be passed only from a defined direction. For example, when you set the edge of a tile that represents a cliff as impassable, characters will be unable to move between that tile and the next tile, creating the sense of height.

Those tiles with marks displayed as arrows pointing in a specific indicate that it is possible to move from that direction, ones without arrows are not passable. Moreover, by changing the parameters of the [Passage] setting, these settings will change automatically.
Ladder

Switch to the editing mode for ladder settings. When you add this parameter, the direction a character using this tile faces will be fixed to up, giving the appearance of going up and down things like ladders and ropes.

Click the marks in the Tile List to change tiles to have this parameter or not. A mark (a ladder) will be displayed on tiles which have this setting.
Bush

Switch to the editing mode for bush settings. When a tile has this setting, 12 pixels from the bottom of characters who cross this tile will appear half transparent, as if their feet are being hidden by dense grass.

However, part of the tile will not become half transparent depending on the image when giving this setting to tiles in [A1] through [A4].

Click the marks in the Tile List to change tiles to have this parameter or not. A mark (two wavy lines) will be displayed on tiles which have this setting.
Counter

Switch to the editing mode for counter settings. When a tile is given this setting, it will start events even when a character and event are not right next to each other, just as when talking to a character with a desk between them.

Also, setting this to the tile in [A2], tiles having this element will be drawn 12 pixels downward.

Click the marks in the Tile List to change tiles to have this parameter or not. Tiles which have this setting have a mark (4-sided diamond) displayed on them.
Damage Floor

Switch to the editing mode for Damage Floors. When a tile is given this setting, characters will receive damage when crossing this tile. This can be used for representing dangerous terrain like poisonous swamps, trees with thorns.

Click the marks in the Tile List to change tiles to have this parameter or not. A mark (two triangles) will be displayed on tiles which have this setting.
Terrain Tag

You can assign values between 0 and 7 to each tile. No specific uses are defined. This value can be retrieved by using the [Get Location Info] event command. Those terrain tags retrieved which are located in upper layers other than zero will be prioritized.
Note

The [Note] section can be used to make notes while making your game.
Right-click to show the menu and choose [Plugin Help...] to display the Plugin Help.


Tileset Details

1 tile is 48x48 in size, and tiles need to be grouped in the 5 types of sets, A through E, below.

Additionally, the specifications for some tiles can change according to the contents set under [Mode] found in [Tilesets] in the database.
Set A

This set will be used as the lower layer when drawing the map. This set is divided further into 5 parts, with most of them being called [Autotiles], which are composed of special tiles that have their boundary lines automatically created.

Autotiles are, as a rule, arranged in a pattern composed of 6 tiles as seen in the illustration below, making up the basic structure of the tiles.

a
    Representative Pattern (for displaying in the tile palette)
b
    Pattern with boundaries at each corner
c
    Group Pattern (refers to group of tiles with one in the center and 1 in each of the 8 directions)

If the autotile located in the (8,8) position from the bottom-right is transparent, that autotile will be evaluated as a "forest type". If a forest tile has the bush element assigned to it, character images will not appear as half transparent in the 8 types of tiles below which includes the bottom right and bottom left boundaries.
Part 1

These are 768x576 in size and made up of the 5-pattern blocks as in the illustration above. Basically, tiles in this part will not have a boundary created even if they touch.
Boats and ships can only travel through the tiles in this part. However, tiles in this tileset will no longer be able to be entered using boats and ships if the tileset is configured to allow players to walk on the tiles.

Block A
    Autotiles used as ocean tiles. By placing 3 autotile basic patterns horizontally in a row, it is possible to animate them.
Block B
    Autotiles used as deep ocean tiles. Boundaries for ocean tiles will be created only when tiles in this block touch tiles in part 1. Tiles in Block A will automatically complete the transparent color of this block. Just like Block A, by placing 3 autotile basic patterns horizontally in a row, it is possible to animate them. Moreover, boats cannot travel through tiles in this block.
Block C
    Autotiles which decorate ocean tiles in Block A. Tiles in Block A will automatically complete the transparent color of this block. Additionally, boats and ships cannot travel through tiles in this block.
Block D
    Autotiles used as water tiles. By placing 3 autotile basic patterns horizontally in a row, it is possible to animate them.
Block E
    Used for waterfall tiles. You can create a group pattern by placing two tiles horizontally, and animate them by placing 3 vertically in a row. Additionally, boats and ships cannot travel through tiles in this block.

Part 2

These are 768x576 in size and composed of 4 2-pattern blocks placed vertically in a row as in the illustration above. Specifications for this part only can change according to the contents set under [Mode] found in [Tilesets] in the database.

If the tiles in this part have the counter element, they will be used as autotiles to create tables, and the bottom of the pattern will be displayed as shifted 12 pixels down when placed.

Block A (Field Type)
    Composed using 4-pattern autotiles, and will be handled as 1 only, 1 and 2 overlapping, 3 only, 3 and 4 overlapping in the actual tileset.

    ↓
Block B (Field Type)
    It is possible to store 4 patterns, and are special tiles that can be placed over tiles in Block A in the actual tileset. 
Block A (Area Type)
    It is possible to store 4 patterns, and are tiles that can be placed over tiles in Block B in the actual tileset. 
Block B (Area Type)
    It is possible to store 4 patterns, and are tiles that can be placed over tiles in Block A in the actual tileset. 

Part 3

Autotiles which will be primarily used for the appearance of buildings. These are 768x384 in size, and are composed by placing 8 tiles horizontally and 4 tiles vertically, formed using only the autotile group pattern.

By placing two or more tiles in this part together vertically when designing your map, shadows will automatically be created on the adjacent touching tile on the right side. However, shadows will not be automatically generated if the adjacent tile belongs to a part other than Part 2 (excluding Block C) or Part 5.
Part 4

Autotiles which will be primarily used for walls. These are also used for walls for dungeon instances. These are 768x720 in size. Composed by placing 8 tiles horizontally and 3 tiles vertically using autotile basic structures and those tiles placed vertically in a row using only the autotile group pattern.

By placing two or more tiles in this part together vertically when designing your map, shadows will automatically be created on the adjacent touching tile on the right side. However, shadows will not be automatically generated if the adjacent tile belongs to a part other than Part 2 (excluding Block C) or Part 5.
Part 5

These are 384x768 in size and please be sure to place the tiles here in an 8x16 arrangement. Tiles contained in this file will all be treated as normal tiles. The 3rd, 5th and 7th tiles from the top are used also for the floors of dungeon instances.
Set B through Set E

These sets will be used as the upper layers when drawing the map.
These are 768x768 in size and be sure to place the tiles here in a 16x16 arrangement.

    Leave the tile located in the top left of Set B blank as this represents nothing being placed in the upper layer.

