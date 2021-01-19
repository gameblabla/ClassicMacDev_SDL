Here, you will find some files and resources on how to develop apps for Mac OS 8.1+ using SDL 1.2.

# Requirements
Retro68 on a Linux, Windows or Mac OSX
Mac OS 8.1+ with a PPC processor (68k on 8.1 was untested, earlier versions are also untested)
StuffIt expander to decompress the archive
MPW header files (you can take them from CodeWarrior)


My makefiles assumes that RETRO68 as an envirionment variable exists.

It should point to :

/to/path/Retro68-build/toolchain/bin

Where your toolchain is.


Make sure to git clone the following repositories :

https://github.com/gameblabla/SDL12_mac

https://github.com/gameblabla/SDL12_mixer_mac

Then use the Makefile.mac to compile it.

To compile it, run make -f Makefile.mac.

You can then compile pretty much most SDL 1.2 apps as long as they don't use timer, threads, OpenGL or joysticks.

(Joystick support can work on 8.5 or later but i wanted to have compatibility with 8.1 so i disabled it, this is something
that you can revert by looking at my changes. I might make 8.5 support optional later)

# Also read

https://nondisplayable.ca/2017/12/20/sdl-on-classic-mac.html

I have compiled SDL 1.2.15 and it doesn't seem to fix the issue with keysym unfortunately.
This could be a regression due to a patch that was merged late in its lifespan related to input, not sure. (See https://github.com/spurious/SDL-mirror/commit/3b3b5c04292e4d6eb8b5a175af1d1990496a3681#diff-98b80a52390da050b6836ce9c3d7248ec4b6378b65e6ddaaaf53f14dda0b9dc9)
It's very possible however, that it was never fixed. You can use scancode as a workaround.

# Other info

SDL's internal file functions handle the conversion from Unix paths to mac but if you are using fopen directly,
you have to do the conversion yourself.
For a relative path, instead of doing "image/log.txt", do instead ":image:log.txt".
If you just want to write a file to the root directory of the executable, "log.txt" will do as well.

SDL 1.2 originally required Mac OS 8.5 but disabling the atomic related functions (in particular in the audio code) allowed it to work on Mac OS 8.1 without ill effects.
