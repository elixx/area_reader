# Area Reader
A Python Library to parse MUD area files and create objects in Evennia

This project reads area files from old MUDs and presents them as Python objects.
The returned objects all use the [Attrs](https://pypi.python.org/pypi/attrs) package so it is very easy to do stuff like render out the entire tree of objects as JSON or similar.

## Example Usage (within Evennia):
```
!
from area_reader.evennia_import import AreaImporter
x = AreaImporter()
x.load("D:/mud-areas/midgaard.are")
x.load("D:/mud-areas/newthalos.are")
x.load('D:/mud-areas/moria.are")
x.spawnRooms()
x.enumerateObjectLocations()
x.spawnObjects()

```
The above will load the ROM area files, and display info about the first room of each area, and any exits that don't link up. Exits with matching `vnum`s that cross areas will link up properly.

Some old area files don't work at all.
I think it may have to do with the original area_reader and handling of ROM area reset commands.
 
I've tested a bunch from https://github.com/vedicveko/Mud-Areas and a list of working ones is available
[here](working_areas.md). 

Make sure you create or redefine `typeclasses.exits.LegacyExit`, `typeclasses.objects.LegacyObject` and `typeclasses.objects.LegacyRoom` in the code.
These are used as bases for objects that the importer created.

Rooms, objects, and exits from each area are tagged and given an attribute 'area' with the area name, to make DB maintenance easier.

 
