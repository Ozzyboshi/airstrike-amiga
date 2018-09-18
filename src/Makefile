CC=m68k-amigaos-gcc
CFLAGS:=  -noixemul -Os -Wall -Wno-unused $(OPTIONS) -fomit-frame-pointer
#
CFLAGS += -I/opt/amiga/SDL_image-pack/include/SDL -I/opt/amiga/include/SDL -Isprite -I. -Isupport -DINLINE=inline
CFILES:= $(shell find . -name '*.c')
OBJECTS:= $(CFILES:.c=.o)

airstrike: $(OBJECTS)
	$(CC) -o $@ $(CFLAGS) $(OBJECTS) -L/opt/amiga/m68k-amigaos/lib -lSDL -ldebug -L/opt/amiga/SDL_image-pack/lib  -lSDL_image -ljpeg -lpng -L/opt/amiga/zlib-package/lib -lz -lm 

airstrike-sound: $(OBJECTS)
	$(CC) -o $@ $(CFLAGS) $(OBJECTS) `sdl-config --libs` -lSDL_image -lSDL_mixer

# Use the rule below when coding new sprite types
#sprites_autogen.h: sprite_types/*.c
#	../utils/genspritelist.sh $^

clean:
	rm -f `find . -name '*.[od]' -or -name '*~' -or -name '*.bb' -or -name '*.bbg'`

dryclean: 
	rm -f `find . -name '*.[^ch]' -type f` 

#Automatic dependency handling. This is not needed for a simple compile.

#include $(CFILES:.c=.d)
#
#%.d: %.c
#	$(CC) -MM $(CFLAGS) $< > $@.$$$$; \
#	sed 's,$(*F)\.o[ :]*,$(@:.d=.o) $@ : ,g' < $@.$$$$ > $@; \
#	rm -f $@.$$$$
