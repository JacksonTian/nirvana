FINAL_CFLAGS = -I../deps/libuv/include
NIRVANA_CC=$(CC) $(FINAL_CFLAGS)
PREFIX?=/usr/local
INSTALL=install
INSTALL_BIN=$(PREFIX)/bin
NIRVANA_INSTALL=$(QUIET_INSTALL)$(INSTALL)

LINKCOLOR="\033[34;1m"
BINCOLOR="\033[37;1m"
ENDCOLOR="\033[0m"

QUIET_INSTALL = @printf '    %b %b\n' $(LINKCOLOR)INSTALL$(ENDCOLOR) $(BINCOLOR)$@$(ENDCOLOR) 1>&2;

all: nirvana-server

dep:
	$(NIRVANA_CC) -MM *.c > Makefile.dep

include Makefile.dep

libuv:
	../deps/libuv/gyp_uv
	make -C ../deps/libuv/out BUILDTYPE=Release

%.o: %.c
	$(NIRVANA_CC) -c $<

# nirvana
nirvana-server: main.o
	@mkdir -p bin
	$(NIRVANA_CC) -o bin/$@ $^ ../deps/libuv/out/Release/libuv.a -framework CoreFoundation -framework CoreServices

clean:
	rm *.o

install:all
	@mkdir -p $(INSTALL_BIN)
	$(NIRVANA_INSTALL) bin/nirvana-server $(INSTALL_BIN)

.PHONY: all nirvana-server dep clean