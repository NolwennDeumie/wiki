---
title: "Onglet Tileset"
description: "Documentation de l'onglet Tilesets pour RPG Maker VX Ace et MV."
og_image: "/assets/default_opengraph.png"
---

Les **tilesets** sont des collections de **tiles** (ou tuiles en Français) qu'on utilise pour créer des **maps**. Avant de rentrer dans le détail de cette catégorie, il vaut mieux parler des **maps** et de certaines spécifications concernant les images utilisées pour créer un **tileset**.

## Qu'est-ce qu'une map ?

Votre jeu se passe dans un certain univers imaginaire, ou basé sur notre réalité. De cet univers est issu un monde, avec sa géographie, ses peuples, ses interactions. Du point de vue du scénariste, ce monde est représenté sous forme de données appelées **maps**. Du point de vue du développeur, les **maps** sont les différents niveaux de jeu que votre joueur va parcourir.

La manière classique de créer une **map** sur RPG Maker est de placer des **tiles** sur une grille. Les **tiles** sont ces petits carrés de texture de 32x32 px (pour Ace) ou 48x48 px (pour MV) visibles dans la partie supérieure gauche de l'éditeur (également appelée palette).

## Spécifications d'une map

### Le rôle des tiles

Les **tiles** sont des images qui sont utilisés pour donner à la **map** son apparence. Ils sont en plus configurés pour être traversables, ou au contraire bloquants, pour le personange et les événements (c'est ce qu'on appelle leur passabilité)

On associe à une **map** donnée un **tileset** : un fichier de données qui regroupe à la fois les iamges des *tiles*, mais également leur passabilité et d'autres données de configuration. Il est possible de changer instantanément l'apparence de la *map* en changeant son *tileset*. On verra plus loin comment on configure un tileset dans la base de données.

Note : il est très facile de faire la confusion entre ce qu'on appelle communément les **tilesets** sur les forums (ces images constituées de plusieurs **tiles**) et ce qu'on appelle **tileset** dans l'éditeur (un fichier de données constitué entre autres de ces images).

### Classification des tiles

Quel que soit l'éditeur utilisé (Ace ou MV), il est possible d'inclure jusqu'à 5 types de **tiles** dans un **tileset**, divisés en 5 onglets A, B, C, D et E. L'onglet A est réservé à la couche inférieure, celle utilisée habituellement pour représenter le sol et les murs. Les onglets B à E sont tous réservés à la couche supérieure, qui sert à placer les éléments de décoration tels qu'arbres et buissons.

Il est tout à fait possible de palcer un tile de couche inférieure et un tile de couche supérieure sur le même emplacement sur la map (dans cet ordre précisément !). Maitriser cette combinaison d'éléments de couche basse et de couche haute eprmet de créer des **maps** très détaillées.

Il a été défini comme standard que :

* les tiles représentant des étendues d'eau, des sols naturels (herbe, terre, sable), les sols et les murs sont réservés à la couche basse (et donc à l'onglet A) ;
* les tiles servant à décorer, embellir les tiles précédents sont réservés à la couche haute (et donc aux onglets B, C, D et E).

Spécificité de RPG Maker MV : il est possible de superposer deux tiles de la couche supérieure l'un sur l'autre pour créer un **tile combiné**. Ceci permet d'apporter plus de variations sur la **map** mais cette utilisation doit s'accompagner de quelques précautions. Ce sera détaillé plus loin.

### Quelques fonctionnalités avancées

* **Les autotiles** : dans l'onglet A de la palette, certains **tiles** ont un comportement particulier. On les appelle des **autotiles**. Ces éléments sont codés de manière à former automatiquement une bordure en fonction de la façon dont ils sont placés. C'est un sacré gain de temps, mais ça peut également être une nuisance. Pour annuler la formation automatique de la bordure, il suffit de maintenir le bouton `Shift` lorsqu'on place l'**autotile**. Ceci conduit à une technique avancée qui sera détaillée plus loin. Pour terminer sur les **autotiles**, ils représentent les sous-catégories A1, A2, A3 et A4 du **tileset** en base de données.

* **Les ombres automatiques** : certains **tiles** de l'onglet A projettent automatiquement une ombre si on en place deux ou plus verticalement. Attention cependant, l'ombre en sera projetée que sur les éléments de la couche basse. Les éléments de la couche haute ne seront pas affectés. Pour rectifier d'éventuelles ombres manquantes (ou pour les retirer), il suffit de sélectionner le `pinceau ombre` dans les outils de dessin et dessiner des ombres supplémentaires. Ce pinceau a la particularité de placer une ombre qui fait 1/4 de la taille d'un **tile**. Pour retirer une ombre, il suffit de cliquer sur l'ombre à retirer avec ce pinceau.

## Spécifications particulières des tiles

### Tiles de la couche inférieure

En réalité, la couche inférieure est composée de deux sous-couches : la *base* et la *couche d'embellissement*. Quasiment l'intégralité des **tiles** de la couche A iront sur la *base*. Les seuls **tiles** concernés par la *couche d'embellissement* sont les tous les **tiles** de la moitié droite de la sous-catégorie A2 du **tileset** en base de données. Ces **tiles** peuvent se placer au-dessus de ceux de la *base*, un peu comme on place habituellement les **tiles** de la couche supérieure sur ceux de la couche inférieure.

En réalité, ceci est le fonctionnement des **tilesets** configurés en mode `REMPLACER` en base de données. Pour tous les **tilesets** configurés avec le mode `World type`, les **tiles** placés en 2ème colonne ou 4ème colonne verront le **tile** de base invariablement changer pour le **tile** de la 1ère colonne ou de la 3ème colonne.

### Tiles de la couche supérieure

De la même manière, on peut considérer que la couche supérieure est composée de deux sous-couches. Ici, elles ne sont pas spécialement nommées, il suffit de se rappeler que lorsqu'on place un **tile** sur un emplacement donné, il va sur la sous-couche la plus haute. S'il y a déjà un **tile**, ce dernier passe sur la sous-couche du dessous et le nouveau prend sa place sur celle du dessus. C'est comme cela qu'on crée des **tiles combinés**.

Si on rajoute un troisième **tile**, celui de la sous-couche inférieure disparait, celui de la sous-couche supérieure passe en dessous et le 3ème **tile** se palce sur la sous-couche supérieure. Sauf si le 3ème **tile** est identique à celui de la sous-couche supérieure, auquel cas il ne se passe rien.

Le fonctionnement est simple, mais il est nécessaire de prendre quelques précautions.

1. TOUJOURS effacer avec le **tile** tout en haut à gauche de l'onglet B. Ne jamais utiliser un autre **tile**, même s'il est lui aussi transparent. Ce fameux **tile** a la propriété de vider intégralement les deux sous-couches à la fois. Par ailleurs, il assure que la passabilité de la **map** à cet emplacement précis sera celle du **tile** en couche basse. À cet effet, NE JAMAIS MODIFIER la passabilité ☆ de ce **tile** spécial.
1. Lorsqu'on combine deux tiles de passabilités différentes, la passabilité qui en résulte est celle du tile le plus en haut.
1. Exception à la règle précédente : si un des deux **tiles** a la passabilité ☆, alors la passabilité résultante sera toujours celle de l'autre **tile**, peu importe lequel est au-dessus et lequel est au-dessous.
1. Enfin, et ceci est une source d'erreurs fréquentes, si le **tile** le plus en dessous a une passabilité ☆ (et que celui au-dessus n'a pas de passabilité ☆), il sera affiché au-dessus en jeu, même s'il apparait bien au-dessous dans l'éditeur !

## Configurer un Tileset en base de données

### Rôle du tileset





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

## Spécifications MV concernant les images

Note : ce qui suit est intégralement dédié à MV. Je laisse qui veut créer les templates pour VX Ace.

### Informations préalables

* un **tile** fait 48x48 px
* les **tiles** doivent être assemblés sous formes d'images constituant 5 groupes : A, B, C D et E
* le groupe A est constitué de plusieurs images et subdivisé en A1, A2, A3, A4 et A5
* la taille des images est fixe

### Groupe/onglet A

Rappel : le groupe A contient l'ensemble des **tiles** qui vont constituer la couche basse d'une **map**

Les images qui constituent les sous-groupes A1, A2, A3 et A4 sont des assemblages d'**autotiles**. Ci-dessous, un **autotile**, un élément constitué en réalité de six **tiles** :

*Image*

* a. l'**autotile** tel qu'il apparait dans la palette (dimensions d'un **tile**)
* b. motif avec les bordures à chaque coin (dimensions d'un **tile**)
* c. motif avec les bordures dans les 8 directions (dimensions d'un carré de quatre **tiles**)

Plus précisément, pour les graphistes, considérez que l'**autotile** est découpé ainsi :




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

