# dmenu - dynamic menu
# See LICENSE file for copyright and license details.

include config.mk

SRC = drw.c dmenu.c stest.c util.c
OBJ = ${SRC:.c=.o}

all: options dmenu stest

options:
	@echo dmenu build options:
	@echo "CFLAGS   = ${CFLAGS}"
	@echo "LDFLAGS  = ${LDFLAGS}"
	@echo "CC       = ${CC}"

.c.o:
	@echo CC $<
	@${CC} -c ${CFLAGS} $<

config.h:
	@echo creating $@ from config.def.h
	@cp config.def.h $@

${OBJ}: arg.h config.h config.mk drw.h

dmenu: dmenu.o drw.o util.o
	@echo CC -o $@
	@${CC} -o $@ dmenu.o drw.o util.o ${LDFLAGS}

stest: stest.o
	@echo CC -o $@
	@${CC} -o $@ stest.o ${LDFLAGS}

clean:
	@echo cleaning
	@rm dmenu stest config.h *.o

install:
	@cp -f dmenu dmenu_path dmenu_run stest /usr/local/bin
	@cp -f dmenu.1 stest.1 /usr/local/man/man1

uninstall:
	@echo removing executables from /usr/local/bin
	@rm /usr/local/bin/dmenu
	@rm /usr/local/bin/stest
	@rm /usr/local/bin/dmen_path
	@rm /usr/local/bin/dmenu_run
	@echo removing manual page from /usr/local/man/man1
	@rm /usr/local/man/man1/dmenu.1
	@rm /usr/local/man/man1/stest.1

.PHONY: all options clean install uninstall