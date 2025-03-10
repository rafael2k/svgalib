#----------------------------------------------------------------------
# Makefile for SVGAlib GL routines.
#----------------------------------------------------------------------

# *** NO SERVICIBLE PARTS HERE!
#     All options are in Makefile.cfg.

include ../Makefile.cfg

srcdir    = ..
VPATH     = $(srcdir)/gl

ifeq (a.out, $(TARGET_FORMAT))
  DEFINES += -DSVGA_AOUT
endif

ifeq (y, $(NO_ASM))
  DEFINES += -DNO_ASSEMBLY
endif

#----------------------------------------------------------------------
# Rules Section
#----------------------------------------------------------------------

MODULES	 = grlib.o driver.o line.o palette.o scale.o text.o font8x8.o \
	   cbitmap.o mem.o 

all:	libvgagl.a
.PHONY: all clean dep

libvgagl.so: libvgagl.so.$(VERSION)
libvgagl.so.$(VERSION): $(MODULES)
	$(CC) -m32 -s -shared -Wl,-soname,libvgagl.so.$(MAJOR_VER) -o libvgagl.so.$(VERSION) \
	  $(MODULES) -L$(srcdir)/sharedlib -lvga
	ln -sf libvgagl.so.$(VERSION) libvgagl.so
	ln -sf libvgagl.so.$(VERSION) libvgagl.so.$(MAJOR_VER)

libvgagl.a: $(MODULES)
	rm -f libvgagl.a
	$(AR) rcs libvgagl.a $(MODULES)

.c.o:
	$(CC) -m32 $(CFLAGS) -c -o $*.o $<

.S.s:
	$(CC) -m32 $(CFLAGS) -E $< >$@

.s.o:
	$(CC) -m32 $(CFLAGS) -c -o $*.o $<

.c.s:
	$(CC) -m32 $(CFLAGS) -S -o $*.s $<

.o:
	$(CC) -m32 $(CFLAGS) $(LDFLAGS) -o $* $*.o $(LIBS)
	chmod 4755 $*

$(MODULES): .depend.gl

dep:
	rm -f .depend.gl
	make depend

.depend.gl:
	echo '# GL Module dependencies' >>.depend.gl
	$(CC) $(INCLUDES) -MM $(patsubst %.o,$(srcdir)/gl/%.c,$(MODULES)) >>.depend.gl

clean:
	rm -f .depend.gl *.bak *.o *~ libvgagl.a libvgagl.so*

#
# include a dependency file if one exists
#
ifeq (.depend.gl,$(wildcard .depend.gl))
include .depend.gl
endif
