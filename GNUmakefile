# Makefile for the supdup server and client.

SHELL = /bin/sh
PREFIX ?= /usr/local

OS_NAME = $(shell uname)
ifeq ($(OS_NAME), Darwin)
OS = OSX
endif

CC ?= cc
CFLAGS = $(shell pkg-config --cflags ncurses 2> /dev/null) -g -Wall
LDFLAGS = -g

# Mac OSX
ifeq ($(OS), OSX)
LDFLAGS = -L/opt/local/lib
endif

# The server isn't ready for prime time.
all:	supdup

SUPDUP_OBJS = supdup.o charmap.o tcp.o chaos.o
supdup: $(SUPDUP_OBJS)
	$(CC) $(LDFLAGS) -o $@ $(SUPDUP_OBJS) $(shell pkg-config --libs ncurses 2> /dev/null || printf '%s' "-lncurses")

SUPDUPD_OBJS = supdupd.o
supdupd: $(SUPDUPD_OBJS)
	$(CC) $(LDFLAGS) -o $@ $(SUPDUPD_OBJS)

install: supdup
	install -m 0755 supdup $(PREFIX)/bin
	test -x supdupd && install -m 0755 supdupd $(PREFIX)/bin

clean:
	rm -f *.o
	rm -f supdup supdupd
