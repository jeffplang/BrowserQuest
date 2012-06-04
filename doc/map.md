Tile properties for tileset "tileset"
-------------------------------------
* c -- collision (blocking) tile
* v -- unknown
* length -- used with the delay property for animated tiles.  Used on its own for ?
* delay -- used for animated tiles.  The value indicates how many milliseconds per frame.  A length property must also be specified, indicating how many subsequent tiles are frames.


Tile properties for tileset "mobs"
----------------------------------
* type -- indiciates monster type.  Corresponds to lowercased entity name in Types.Entities object in shared/gametypes.js


Intermediate JSON file
----------------------
A fairly straightforward translation of XML contained in TMX file to JSON.
TODO: More details


Client Map File Notes
---------------------

**Cliet map JSON has the following keys:**

###animated

An array of tile indeces in `data` of tiles that are animated

###blocking

An array of tile indeces in `data` of tiles that are non-walkable

###checkpoints

###collisions

An array of tile indeces in `data` of tiles that produce a collision

###data

The big one: an array with length `height * width`, a tileID to represent each worldmap tile.  Tile [0,0] is in the upper left corner of the worldmap

###doors

###height

The height of the worldmap in tiles

###high

###musicAreas

###plateau

###tilesize

###width 

The width of the worldmap in tiles