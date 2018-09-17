### Airstrike amiga
This is a port of a game I found on the Debian repository called airstrike.
The port is intended to run in an high end Amiga RTG system like a Vampire.
The game was compiled with bebbo's gcc compiler and some libsdl1.2 for amiga curtesy of EAB Amigadev group (THX Marlon).
To ease the build process i built a docker container so, to get new executables just type:

docker run -v #PUTHEREAIRSTRIKE-AMIGAPATH#/:/data -w /data -t  --rm ozzyboshi/bebbo-amiga-gcc make
At the end of the process a new executable file called airstrike is created on the root dir.
At this stage no sound is implemented and the game is pretty slow, looking for help to improve performances.

Home page of the original game : http://icculus.org/airstrike/

![Screenshot](https://i.ytimg.com/vi/C3mebohbiYk/hqdefault.jpg)
