# acplay
Animal Crossing time scheduled music player

Written in `bash`, using `vgmstream` and `sox`.

## Description
A `bash` script that, when used the right way, plays the Animal Crossing background music, hour by hour, on real time.
Made to play the game's stream files (usually .bcstm) using the `vgmstream` 'test' binary. If you prefer some dirty pre-looped mp3 or to not use `vgmstream`, then ok, you can grab the last lines of the script, remove the `vgmstream` part, and you're ready to go.

Of course, I won't provide any music files.

They're Nintendo's Copyright.

## Installation
First, grab that `acplay` file. It's a `bash` script, so you can append `.sh` to it if you want.

Now, the dependencies. They're `vgmstream` and `sox`.

### vgmstream
Thanks to *Halley's Comet Software* for supporting the `vgmstream` project. It is available here:
> https://hcs64.com/vgmstream.html

On **macOS**, it is not necessary to compile it yourself. You can

    brew install vgmstream

### sox
Install `sox` with your favourite package manager. If it's not available this way, then head to this page:

> http://sox.sourceforge.net

## Setting up
It's a little complex to 'set up', but it should be understandable by reading the script.

First, you should have some files to play. It is recommended to have at least 24 of them. Any other way, wouldn't it be a little bit nonsense to play 24h music?

The files should be somewhat similar to the following hierarchy:
```
/path/to/ANIMAL_CROSSING
├── GAME_FOLDER_1
│   ├── FILE_00.bcstm
│   ├── ...
│   ├── FILE_24.bcstm
│   ├── ANOTHER_FILE.bcstm
│   └── THIS_FILE_DOESNT_MATTER.txt
├── GAME_FOLDER_2
│   ├── FILE_12_AM_SUNNY.brstm
│   ├── FILE_12_AM_RAINY.brstm
│   └── ...
└── ...
```
It's pretty logical if you like the game so much to have dedicated folders to their files.

There, you can name ANIMAL_CROSSING as you please. For example, the default in the script was named `ac`.
Its path is specified at the start of the script.
The directories inside it should be named in some easy-to-remember way, as based on that you'll specify a game in the command line. For instance, the defaults in the script (it's how do I use it) are `cf` for City Folk, `nl` for New Leaf, and `mk` for the Mario Kart 8's DLC.

Each folder for a game should contain the files to be played hour by hour. Do you know the `date` command? It uses `strftime(3)` to parse the time. Well, that's what the script uses. There's a section in the script which specifies in what format are the files arranged, using those `%`. The default one is a good example, because it contains cases for no-padding (I never rename the files). And it uses a... little tweak about variables (i don't like how it is), to specify each case for the weathers (sunny, rainy and snowy). But it works well if you don't have all the weathers, as long as you specify the cases there.

The THIS_FILE_DOESNT_MATTER.txt means that you can have any unplayable-by-vgmstream files there, too. No problem. The script, in any non-standard behaviour, will iterate through every file testing it with vgmstream until a match is found, and then determine wheter to play continuously or one-play, depending on the file's ability to be looped.

## Usage
```bash
acplay [options] [game]
```

For info about the `game`, refer to the previous section, please. Just try to have your things properly saved.

```
Options:
-h        show this helpful (questionable) info
-l        just list the available music. 
-p query  just find and play the specified music.
-q        play quietly; no progress from 'play'.
-r        just play a random music.
-w  num   weather, when available [1(SUNNY)|2(RAINY)|3(SNOWY)]
```

The behaviours are described below:
* Using no options outside `-h`, `-q` , and `-w`, and no game, the script plays the nice background music that many would like. That from the 'default' game, specified at the first lines of the script. That unless a game is specified.
* Using any of the options `-l`, `-p`, or `-r`, and no game, the script acts over the main folder, not a specific game, unless a game is specified. If there are more than one of such options, the one to take place will be the first alphabetically (that is, `-l`, `-p`, and `-r`). Then the script will exit.
  * `-l` lists the playable files by vgmstream.
  * `-p` requires and argument, that is a query to `find` a playable file. Only the first one to be found will be played. If no results, then `exit 1`.
  * `-r` lists all the files, then plays the playable ones, but sorted randomly with a bit (maybe more bits) of `bash` magic. The same error that for `-p` if there're no files. I forgot to mention that the script determines whether the file has a loop or not. If it has, the loop will continue until you interrupt the script (with `^C`, for example).

## Some notes

I recommend to modify this script as much as you can before using it. Mainly because it's not very probable for you and me to be in the same cirqumstances (in the terms of the needings of this script's behaviour, the files and such).

If you really feel that you need help (for example, if you need something like this but do not know how to do it or do not understand it at all)... try to contact me in any way. Literally. It'd be easy, as I'm not a paranoic about my info inside the Internet.
