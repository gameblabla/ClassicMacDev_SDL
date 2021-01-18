Here, you will find some files and resources on how to develop apps for Mac OS 8.1+ using SDL 1.2.

# Requirements
CodeWarrior 5+ (i only had some luck with CodeWarrior 5 but later versions should work)
32MB of RAM (for CW5, possibly more for later versions)
Mac OS 8.1+ with a PPC processor (68k on 8.1 was untested)
StuffIt expander to decompress the archive

Don't use JIT for Sheepshaver : it will prevent you from compiling large packages like SDL from source !

# Installation

Decompress SDL_binaries.sit with StuffIt Expander and put the SDL folder somewhere.
When you create a new project, make sure to :
- Import QuickTimeLib and StdcLib (or stdlib, forgot) from Codewarrior's Support lib folder. You can find it with Sherlock.
- Add all of the libraries in your project.
- Add the include folder in the Project's settings.
- Make sure to increase the heap to 4096 in your project's settings.

Assuming you don't have any issues with CodeWarrior's headers themselves, you should be good.
For Worship Vector, i had to disable the code related to wchar_t before it would compile properly.

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

SDL 1.2 originally required Mac OS 8.5 but disabling the atomic related functions (in particular in the audio code)
allowed it to work on Mac OS 8.1 without ill effects.
