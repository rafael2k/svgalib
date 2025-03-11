CFLAGS ?= -g -Wall

all = vbetest mode3 vga_reset vbemodeinfo dosint

%.o: %.c
	$(CC) -c $(CPPFLAGS) $(CFLAGS) -o $@ $<

all: $(all)

vbetest: vbetest.c
	$(CC) $(CPPFLAGS) $(CFLAGS) -o $@ $^ -lx86

mode3: mode3.c
	$(CC) $(CFLAGS) -o $@ $^ -lx86

dosint: dosint.c
	$(CC) $(CFLAGS) -o $@ $^ -lx86

vbemodeinfo: vbemodeinfo.c
	$(CC) $(CFLAGS) -o $@ $^ -lx86

vga_reset: vga_reset.c
	$(CC) $(CFLAGS) -o $@ $^ -lx86

install: mode3 vga_reset
	install mode3 /sbin
	install vga_reset /sbin

.PHONY: clean
clean:
	rm -f $(objects) $(all) core regs-out *.bak

.PHONY: distclean
distclean: clean
	rm -f .depend

.PHONY: depend
depend: $(sources)
	-$(CC) -M $(CPPFLAGS) $^ >.depend
