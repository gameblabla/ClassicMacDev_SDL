Here, you will find some files and resources on how to develop apps for Mac OS 8.1+ using SDL 1.2.

# Requirements
Retro68 on a Linux, Windows or Mac OSX
Mac OS 8.1+ with a PPC or M68K processor (m68k support was only tested on several emulators)
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

To compile it, run make -f Makefile.mac for PPC and make -f Makefile.macm68k for M68k.

You can then compile pretty much most SDL 1.2 apps as long as they don't use timer, threads, OpenGL or joysticks.

(Joystick support can work on 8.5 or later but i wanted to have compatibility with 8.1 so i disabled it, this is something
that you can revert by looking at my changes. I might make 8.5 support optional later)

# Ports

I will also post my ports that use SDL 1.2 for Mac OS classic here.

- Worship Vector (PPC & M68k)
(Source code : https://github.com/gameblabla/worship-vector/tree/macosclassic)

The M68k version supports only 640x480 8bpp whereas the PPC version supports all of the resolutions.
Of course, you may want to decrease your monitor's resolution for the PPC version if it ends up being too slow.

- Ganbare Natsuki-San (PPC)
No MIDI playback (it doesn't seem to work at all) but sound effects still.
It might require a G3 or even a G4 despite running at 8bpp.

# Also read

https://nondisplayable.ca/2017/12/20/sdl-on-classic-mac.html

This guy encountered an issue with keysym not working properly with SDL 1.2.15.
I could confirm this issue happens when the code is compiled with CodeWarrior but it doesn't happen with Retro68 !

Some of the keyboard inputs however, don't seem to be mapped like expected but some others do.

# Other info

SDL's internal file functions handle the conversion from Unix paths to mac but if you are using fopen directly,
you have to do the conversion yourself.
For a relative path, instead of doing "image/log.txt", do instead ":image:log.txt".
If you just want to write a file to the root directory of the executable, "log.txt" will do as well.

SDL 1.2 originally required Mac OS 8.5 but disabling the atomic related functions (in particular in the audio code) allowed it to work on Mac OS 8.1 without ill effects.
