## About

**minecraft-data-utils** is a collection of bash and python scripts to parse data from the minecraft player and region files into yaml format.

There are also quick and dirty *yaml2json* and *json2yaml* scripts included.

## Important Notes

Most of these scripts **will leave cached .yaml files** sprinkled around your minecraft world directory.

This is so you can run the slow scripts much faster on subsequent runs since only changed files have to the be reread usually.

## Requirements

* typical linux environment utilities (grep, etc)
* Python Modules (sudo apt-get install python-pip):
	* **nbt2yaml** (sudo pip install nbt2yaml)
	* **nbt** (sudo pip install nbt)
* **bash**
* **pcregrep** (only used in playerBasics2yaml, can probably be worked around in the future)

## Installation

1. Install the prerequisites from **Requirements** above
2. Download the scripts
3. Put all the scripts in the same directory (since most reference each other)
4. Chmod them +x or 755
5. Dance a jig.

## Usage

### Primary

* **namedEntities2yaml** - Parses either a list of regions (*.mca files) or a "world" directory for the locations of all named entities (things you've put a name tag on, like your horse).
	* Never lose your pet again!
* **countEntities2yaml** - Gets a count of entities in every chunk within a list of regions (*.mca files) or a "world" directory. 
	* This is really useful to find out where someone has been camping a zombie spawner for waaaay too long, or spawned too many chickens, and is overloading your server.
* **apiplayer2yaml** - Gets usernames from player.dat UUIDs, caches the results for next time unless it's been more than 1440 minutes, then we recheck mojang's api.
* **player2yaml** - Reads player.dat file, dumps out yaml of information including location, name from *apiplayer2yaml* output, and last active timestamp.
* **level2yaml** - Reads level.dat files, dumps out contents as yaml

### Subsets, Supersets, Wrappers

##### Subsets
* **playerBasics2yaml** - Reads player.dat file (via *player2yaml*) but returns only a subset of the data needed for mapping: location, name, and last active timestamp

##### Supersets
* **allplayer2yaml** - Runs *player2yaml* for all players, returns proper yaml
* **allplayerBasics2yaml** - Runs *playerBasics2yaml* for all players, returns proper yaml

##### Simple Wrappers
* **namedEntities2json** - Returns *namedEntities2yaml* output as json
* **allpayer2json** - Returns *allplayer2yaml* output as json
* **player2json** - Returns *player2yaml* output as json
* **playerBasics2json** - Returns *playerBasics2yaml* output as json
* **allplayerBasics2json** - Returns *allplayerBasics2yaml* ouput as json
* **level2json** - Returns *level2yaml* ouput as json

### Helpers

* **yaml2json** - Reads yaml from STDIN, outputs json to STDOUT
* **json2yaml** - Reads json from STDIN, outputs yaml to STDOUT

## Future

* Will eventually replace all the bash scripts with more robust and performant python versions.
* Streaming yaml2json and json2yaml instead of reading everying in before parsing.

## Thanks

* **[nbt2yaml](https://pypi.python.org/pypi/nbt2yaml)** Awesome util.
* **[NBT](https://pypi.python.org/pypi/NBT)** The python library we use to parse most of the data.
* **[mapcrafter](http://mapcrafter.org)** (*[github](https://github.com/mapcrafter/mapcrafter)*) The reason I wrote these utils was to get extra details onto the map with *mapcrafter-markers-helper*

## Related

* **[mapcrafter-markers-helper](https://github.com/jamcole/mapcrafter-markers-helper)** Put player locations and named entity locations on your mapcrafter map.