execgamesdir = $(prefix)/games
execgames_PROGRAMS = robotfindskitten robotfindskitten-de robotfindskitten-es

robotfindskitten_SOURCES = robotfindskitten.c
robotfindskitten_CPPFLAGS = -DSYSTEM_NKI_DIR=\"$(datadir)/games/robotfindskitten\"
#robotfindskitten_LDADD = -lncurses

# German variant: translated UI, reads its own (German) NKI directory by default
robotfindskitten_de_SOURCES = robotfindskitten.de.c
robotfindskitten_de_CPPFLAGS = -DSYSTEM_NKI_DIR=\"$(datadir)/games/robotfindskitten-de\"

# Spanish variant: translated UI, reads its own (Spanish) NKI directory by default
robotfindskitten_es_SOURCES = robotfindskitten.es.c
robotfindskitten_es_CPPFLAGS = -DSYSTEM_NKI_DIR=\"$(datadir)/games/robotfindskitten-es\"

# Run a static type check on the code
cppcheck: robotfindskitten.c
	cppcheck -I .. --template gcc --enable=all robotfindskitten.c

SPLINT_SUPPRESSIONS = +charintliteral +charindex
splint:
	splint +quiet +posixlib $(SPLINT_SUPPRESSIONS) -I .. *.c
