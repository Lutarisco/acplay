# acplay
Animal Crossing time scheduled music player

Written in `bash`, using `vgmstream-cli` and `bc`. Playable using `sox`

## Description
A `bash` script that, when used the right way, plays the Animal Crossing background music, hour by hour, real time.
Made to loop the game's stream files (bcstm, brstm, et cetera) using the `vgmstream-cli` binary.

## Dependencies
### vgmstream-cli
Thanks to *Halley's Comet Software* for supporting the `vgmstream` project. It is available here:
> https://hcs64.com/vgmstream.html
### bc
Available with most UNIX systems, for doing... math.

### sox
You only need this to play that data this program outputs. That means almost always. The only side case I can think about is to broadcast an Internet radio, e.g. with Icecast.
Install `sox` with your favourite package manager. If you can't, then head to this page:
> http://sox.sourceforge.net

## Setting up
I tried to make this as simple as possible.
First, you should have some special files to play. It is recommended to have all 24 of them (one per hour), and optionally the different weather variations. They come in "stream" files, commonly ripped directly from the games' files, or created by the community. I will NOT provide these files as I'm not of the legal repercussions of doing so.

The filenames should all be named correctly, as per the format inside the script (you can change this!).
And please take your time to change in the script the path to those files as well.
```
/path/to/Animal Crossing/ACCF
├── 00_RAINY.brstm
├── 00_SNOWY.brstm
├── 00_SUNNY.brstm
├── 01_RAINY.brstm
├── ...
└── 23_SUNNY.brstm
```
The specified folder should contain the folders containing the files to be played hour by hour, separated by their game. Different weathers are optional, of course. Do you know the `date` command? It uses `strftime(3)` to parse the time. Well, that's what the script uses. There's a section in the script which specifies in what format are the files arranged, using those `%`. The default one is a good example.

You can also have an audio file with a chime to play at every hour.

And you can set the seconds of fade-out before the next hour arrives with the `fade` variable.

## Usage
```bash
acplay cf snowy | play --ignore-length -
```
The first argument is required and has to match one of the games you have the files for. The second argument is optional and states the weather you'd like to hear from, defaulting to SUNNY. These arguments are case insensitive.

I recommend to modify this script as much as you can before using it, because it's not very probable for you and me to be in the same circumstances.

If you really feel that you need help (for example, if you need something like this but do not know how to do it or do not understand it at all)... try to contact me in any way.
