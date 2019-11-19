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
You only need this to play that data this program outputs. That means always.
Install `sox` with your favourite package manager. If you can't, then head to this page:
> http://sox.sourceforge.net

## Setting up
It's more simple than ever to use this script.

First, you should have some files to play. It is recommended to have all 24 of them (one per hour). They come in "stream" files, commonly ripped directly from the games' files.

The files filenames should all be named correctly, as per the format inside the script (you can change this!).
And please take your time to change in the script the path to those files as well.
```
/path/to/AC/
├── 00.brstm
├── ...
└── 23.brstm
```
The specified folder should contain the files to be played hour by hour. Do you know the `date` command? It uses `strftime(3)` to parse the time. Well, that's what the script uses. There's a section in the script which specifies in what format are the files arranged, using those `%`. The default one is a good example.

## Usage
```bash
acplay | play --ignore-length -
```
I recommend to modify this script as much as you can before using it. Mainly because it's not very probable for you and me to be in the same cirqumstances (in the terms of the needings of this script's behaviour, the files and such).

If you really feel that you need help (for example, if you need something like this but do not know how to do it or do not understand it at all)... try to contact me in any way. Literally. It'd be easy, as I'm not a paranoic about my info _inside_ the Internet.
