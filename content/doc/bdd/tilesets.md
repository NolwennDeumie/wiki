---
title: "Onglet Tileset"
description: "Documentation de l'onglet Tilesets pour RPG Maker VX Ace et MV."
og_image: "/assets/default_opengraph.png"
---

Les **tilesets** sont des collections de **tiles** (ou tuiles en Français) qu'on utilise pour créer des **maps**. Avant de rentrer dans le détail de cette catégorie, il vaut mieux parler des **maps** et de certaines spécifications concernant les images utilisées pour créer un **tileset**.

## Menu

* [Qu'est-ce qu'une map ?]({{< ref "#qu-est-ce-qu-une-map" >}})
* [Spécifications d'une map]({{< ref "#spécifications-d-une-map" >}})
* [Spécifications particulières des tiles]({{< ref "#spécifications-particulières-des-tiles" >}})
* [Configurer un Tileset en base de données]({{< ref "#configurer-un-tileset-en-base-de-données" >}})
* [Spécifications MV concernant les images]({{< ref "#spécifications-mv-concernant-les-images" >}})

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

*Note : ce qui suit est intégralement dédié à MV. Je laisse qui veut créer les templates pour VX Ace.*

**Accès rapide**

* [Groupe A (onglet A) - image A1]({{< ref "#groupe-a-onglet-a-image-a1" >}})

### Informations préalables

* un **tile** fait 48x48 px
* les **tiles** doivent être assemblés sous formes d'images constituant 5 groupes : A, B, C, D et E ;
* le groupe A est constitué de plusieurs images et subdivisé en A1, A2, A3, A4 et A5 ;
* les groupes B, C, D et E sont tous constitués d'une seule image ;
* la taille des images est fixe et dépend du groupe auquel elles sont associées (*voir tableau*) ;
* un tileset n'a pas à contenir la totalité des images A1, A2, A3, A4, A5, B, C, D et E ;

Pour rappel, ce qu'on appelle communément **tileset** sur les communautés et ce que le logiciel considère comme un **tileset** sont deux choses différentes. Quand on parle de **tilesets** sur les communautés, on parle des images A1, A2, A3, A4, A5, B, C, D et E. Le **tileset** du logiciel est constitué de ces images ET de données supplémentaires.

{{< figure src="/images/doc/bdd/tileset-editeur-MV.PNG" alt="Capture d'écran de l'onglet Tileset de RPG Maker MV montrant que le tileset est composé d'images pour les groupes et sous-groupes A1, A2, A3, A4, A5, B et C. Les groupes D et E n'ont pas d'images associées." caption="Ici, on voit que le tileset intitulé SF Outside est constitué de 7 images et contient des données supplémentaires pour chaque image, configurables grâce aux boutons de droite. On peut également associer un mode et des notes au tileset." >}}

### Les trois types d'autotile

Un **autotile** est un **tile** spécial qui va changer d'apparence en fonction des **tiles** qui l'entourent. Si sur la palette de l'éditeur, on ne voit qu'un **tile** de 48x48 px, en réalité sur l'image, il sera constitué de plusieurs **tiles**. C'est el logiciel qui définira quels **tiles** il placera de manière automatique.

Il y a trois types d'**autotiles** sur MV : 

* l'**autotile** classique, qui est utilisé pour faire des bordures, des chemins, couvrir de grandes zones de tapis ou d'herbes hautes ;
* l'**autotile** de mur, qui est essentiellement utilisé pour placer les murs et les toits en pente ;
* l'**autotile** de cascade, qui a un fonctionnement un peu différent des deux autres.

L'**autotile** le plus classique est constitué de 6 **tiles**.

{{< figure class="align-left" src="/images/doc/bdd/tileset-autotile-classique-MV.PNG" alt="" caption="Dimensions totales : 96x144 px." >}} 

1. Ce **tile** n'est pas utilisé par le logiciel. Il sert uniquement de repère dans la palette pour identifier rapidement l'**autotile**. Vous pouvez donc le modifier à votre convenance (on peut, par exemple, lui ajouter une icone Poison si le terrain inflige des dégâts).
1. Ce **tile** sert à faire les coins intérieurs (angles rentrants). 
1. Ce groupe de 4 **tiles** sert à la fois à faire les coins extérieurs (angles saillants), les bordures et le motif interne.

<div style="clear:both;"></div>

Ce qui intéresse donc les graphistes, ce sont le **tile** 2 et les **tiles** 3a, 3b, 3c et 3d. En pratique, quand le logiciel place un morceau d'**autotile** sur la map, il ne choisit pas directement un de ces 5 tiles. Il découpe au préalable chaque **tile** en quatre et reconstitue un **tile** à partir de quatre morceaux. Le véritable template d'un **autotile** ressemble à ceci :

{{< figure src="/images/doc/bdd/tileset-template-autotile-classique-MV.PNG" alt="" caption="TEMPLATE - Dimensions d'un morceau d'autotile : 24x24 px." >}}

Ce template montre bien comment le logiciel découpe les **tiles** en morceaux de 24x24 px. Chaque morceau est affecté à un "coin" du **tile** reconstitué (symbolisé par les petites flèches). 

{{< figure src="/images/doc/bdd/tileset-template-autotile-classique-MV-exemple.PNG" alt="" caption="Exemples de reconstitution de tiles à partir d'un autotile. En vert : sous-unités utilisées pour le motif central. En bleu, sous-unités utilisées pour les bordures. En rouge, sous-unités utilisées pour les coins externes et internes." >}}

Les plus observateurs auront remarqué qu'il y a un pixel mis en évidence sur le template en bas à droite. Il a un rôle particulier, ce sera expliqué plus loin.

{{< figure class="align-right" src="/images/doc/bdd/tileset-autotile-mur-MV.PNG" alt="" caption="Dimensions totales : 96x96 px." >}}

L'**autotile** de mur ressemble beaucoup à l'**autotile** classique, mais il n'a ni **tile** qui sert de repère, ni bloc réservé aux coins internes. Ceci s'explique par le fait que le mapping avec ce type d'**autotile** se fait en colonne uniquement. Au niveau du logiciel, il est constitué de quatre **tiles**, eux-mêmes subdivisés en quatre morceaux. Le **tile** qui sert de repère dans la palette est constitué des 4 morceaux qui forment les 4 coins.

<div style="clear:both;"></div>

{{< figure src="/images/doc/bdd/tileset-template-autotile-mur-MV.PNG" alt="" caption="TEMPLATE - Dimensions d'un morceau d'autotile : 24x24 px." >}}

Enfin, l'**autotile** de cascade ne fonctionne absolument pas comme les deux autres. Il est constitué de deux **tiles**, eux-mêmes subdivisés en *deux* morceaux de 24x48 px, et pas en quatre morceaux. En particulier, cet **autotile** n'a pas de bordures en haut et en bas et n'a pas de coins.

{{< figure src="/images/doc/bdd/tileset-template-autotile-cascade-MV.PNG" alt="" caption="TEMPLATE - Dimensions d'un morceau d'autotile : 24x48 px." >}}




### Notes personnelles

* l'élément du haut de l'autotile ne sert vaiment que pour l'affichage dans la palette, aucun intérêt d'y toucher (on peut donc dessiner des symboles dessus)
* un tile d'autotile est en fait constitué de 4 sous éléments, des mini-tiles de 24x24 px. Ces mini-tiles sont représentés sur les 5 carreaux restants de l'autotile
* j'ai un exemple d'autotile qui montre les sous-éléments.

* le coup de l'autotile de type foret, ça a l'air de marcher une fois tous les 36 du mois... je n'arrive pas à le tester
* réussi ! marche à suivre : recréer le tileset pour que le fichier json je suppose s'actualise. Le truc pas chiant du tout
* le type forêt marche sur absolument tous les types d'autotiles, même les sols pleins !
* le pixel en question est bien celui en (8,8) à partir du coin bas droit du groupe de 6 tiles
If the autotile located in the (8,8) position from the bottom-right is transparent, that autotile will be evaluated as a "forest type". If a forest tile has the bush element assigned to it, character images will not appear as half transparent in the 8 types of tiles below which includes the bottom right and bottom left boundaries.

* il y a une erreur dans l'aide : les éléments du groupe 2, bloc A, ne peuvent pas se superposer à ceux du bloc B, même si al transparence est ajoutée
* pour world type, il y a encore une subtilité, mais ça ne concerne que le bloc A : la deuxième colonne et la 4eme colonne aparessent sur la palette comme un mix de 1+2 et de 3+4. Sur la map, cela fait aussi un tile combiné => autorise de la transparence, mais en réalité si 1 ou 3 n'est aps transparent, le tile combiné ne sera pas transparent.
* j'avoue que je ne vois aps bien l'intérêt...
* je viens d'en saisir l'intérêt : c'est pour fusionner les autotiles de al couche de base, sinon ça ferait des bordures !

* note que ce mécanisme s'applique aussi pour la couche A1, il y a une sorte de mécanisme d'embellissement pour le premier autotile et ses ambellissements
* l'autotile de cascade est particulier, à tester

* pour les autotiles de murs/toits, c'est le même système en sous-tiles de 24x24 px MAIS 1) il n'y a plus le bloc pour les coins inversés et 2) la représentation se fait avec les coins du gros bloc de 4.
* pour faire des coins inversés, on passera par des éléments des onglets B, C, D et E.
* le placement est également altéré : ça fonctionne par colonnes
* quand on peint avec le pinceau, une fois qu'on a fini une colonne, ne pas hésiter à repasser el pinceau dans el sens opposé pour que l'autotile se forme bien ! Sinon il laisse les bords et n'affiche pas le motif central, sauf étrangement pour l'extrémité pour laquelle on a fini de peindre...
* étrangement, ce problème en se pose pas quand on utilise l'outil rectangle ou l'outil remplissage...

* les toits du groupe A4 ont à nouveau l'autotile en 6 : on peut faire des coins inversés avec.
* ceux-là sont réservés pour tout ce qui n'est aps toit en pente, en réalité.

* **Au total, il y a 3 types d'autotiles : ceux en 5 blocs, ceux en 4 blocs (murs et toits en pente) et ceux en bandes (cascades)** Seuls les autotiles du bloc A2 peut être de type alternatif forêt d'après mes tests. à vérifier s'il y a une erreur.

* avec l'astuce du shift, on peut utiliser les autotiles pour obtenir 4 façons d'animer des objets de 1 tile de dimension (par défaut, shift enfoncé, tous les angles internes et enfin bords). C'est aps pratique, mais c'est faisable !
* les cascades n'offrent que 2 alternatives mais sont beaucoup plsu faciles à placer. Et souvent considérées comme des palces perdues sur le tileset

### Groupe A (onglet A) - image A1

Ce groupe de **tiles** est constitué uniquement d'**autotiles** animés (à deux exceptions près). Les **autotiles** animés sont simplement créés à l'aide de trois **autotiles** non animés. Le logiciel gère seul l'animation en 3 frames, c'est à dire qu'il va boucler automatiquement entre les trois variations de l'**autotile** en jeu.

L'image A1 est de dimensions 768x576 pixels et est assez complexe, il faut bien placer les autotiles au bon endroit pour avoir un rendu correct en jeu.

{{< figure src="/images/doc/bdd/tileset-template-A1-MV.PNG" alt="" caption="TEMPLATE - Dimensions totales : 768x576 px. En vert, éléments servant à décorer la couche basse. En bleu, éléments servant à embellir la couche basse. En rose, autotiles de cascade." >}}

Par convention, aucun de ces **autotiles** ne devrait être passable pour un personnage à pieds. Les **autotiles** des sets A et D sont les seuls **tiles** à laisser passer les barques et les bateaux. Le set B autorise le passage des bateaux mais interdit le passage des barques. Tous les autres **tiles** du **tileset** (donc les sets C et E et tout ce qui est contenu dans les groupes A2, A3, A4, A5 et même les groupes B, C, D et E) ne peuvent laisser passer ni les barques, ni les bateaux !

Cependant, si vous choisissez de rendre les **autotiles** des sets A, B et D passables pour le personnage à pieds, alors ils deviendront bloquants pour les bateaux et les barques.

Compléments d'information :

* le set A est habituellement réservé au **tile** d'océan. Notez que **tile** est au singulier : ce sont des **autotiles** animés, il faut donc 3 **autotiles** pour faire une animation.
* le set B sert à embellir le set A : sa texture viendra se superposer à celle de l'**autotile** du set A. Ceci permet d'apporter des variations à l'**autotile** A pour que la carte ne soit pas trop monotone. De plus, appliquer cette texture empèchera les barques de passer, mais autorisera toujours les bateaux à passer. Habituellement, on considère que c'est l'**autotile** animé représentant l'eau profonde.
* les deux sets C servent également à embellir le set A. La différence est que ces deux **autotiles** ne sont pas animés. De plus, appliquer ces textures empêchera tout passage de barques ou de bateaux.
* les six sets D sont semblables au set A : ils représentent habituellement une texture d'eau animée. Il n'est pas possible de les embellir avec les textures des sets B et C.
* les six sets E sont habituellement réservés aux cascades. Ils sont composés de trois templates de cascade présentés plus haut empilés verticalement. Là encore, ces **autotiles** interdisent le passage des barques et des bateaux.

| Set | barque | bateau | couche inférieure utilisée | animation |
|---|---|---|---|---|
| A | passable | passable | base | oui |
| B | X | passable | embellissement | oui |
| C | X | X | embellissement | X |
| D | passable | passable | base | oui |
| E | X | X | base | oui |

**Astuce pour les graphistes** : il est tout à fait possible de détourner l'utilisation de ces **autotiles** animés pour créer de petits objets animés sur la map. L'intérêt est de réduire le nombre d'événements purement décoratifs. L'**autotile** classique permet par exemple de stocker jusqu'à cinq objets et l'**autotile** de cascade permet d'en stocker deux. Pour utiliser cette astuce, il faut au préalable être à l'aise avec la technique du `clic droit` puis `Shift+clic gauche`. 
*Cette astuce mériterait son propre tutoriel.*











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

