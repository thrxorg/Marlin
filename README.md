# Marlin 3D Printer Firmware
<img align="right" src="../../raw/1.1.x/buildroot/share/pixmaps/logo/marlin-250.png" />

## Marlin 1.1.9

### Reduce Size
Taken from:
https://thborges.github.io/blog/marlin/2019/01/07/reducing-marlin-binary-size.html


How to reduce the Marlin binary size? Here are my special compilation flags that were able to reduce it by almost 6K.

Changing them is easy wether you are using Arduino IDE or PlataformIO. 

If already using PlataformIO, it is easier. Just create a new build target in platformio.ini, copying the original config for your printer board and adding the new flags:

```
build_unflags = -g -ggdb
build_flags   = ${common.build_flags} -fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues
```

In Arduino IDE, you should edit the file platform.local.txt for your board. It is inside the hardware folder, together with your other Arduino project folders, or in the Arduino instalation folder. Search for it.

Content to add in platform.local.txt:
```
compiler.c.extra_flags=-fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues
compiler.cpp.extra_flags=-fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues
compiler.c.elf.extra_flags=-Wl,--relax
```

Not that you should, but you can even try more aggressive optimizations supposed to change a little the printer execution time for some routines:

```
-finline-limit=3 -ffast-math
```

Some of my sizes using PlatformIO when compiling Marlin 1.1.9 for my customized version of an Anet A8 with filament runout sensor, bed probe, graphical display, wifi and others:

| Size (bytes) | Options |
|--------------:|:---------|
| 125216 | Default flags |
| 124240 | -fno-tree-scev-cprop -fno-split-wide-types |
| 123324 | -fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax |
| 119730 | -fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues |
| 118872 | -fno-tree-scev-cprop -fno-split-wide-types -Wl,--relax -mcall-prologues -finline-limit=3 -ffast-math |

You can verify what each of these options do in avr-gcc man page or online at [avr-gcc manpage](http://ccrma.stanford.edu/planetccrma/man/man1/avr-gcc.1.html).

