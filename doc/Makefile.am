info_TEXINFOS = multiboot.texi
EXAMPLES = boot_i386.S boot_mips.S kernel.c multiboot2.h
multiboot_TEXINFOS = boot_i386.S.texi boot_mips.S.texi kernel.c.texi multiboot2.h.texi
SRC2TEXI = src2texi
noinst_SCRIPTS = $(SRC2TEXI)
EXTRA_PROGRAMS = kernel
pkginclude_HEADERS = multiboot2.h

# The example kernel is built if you specify --enable-example-kernel.
if BUILD_EXAMPLE_KERNEL
noinst_PROGRAMS = kernel
kernel_SOURCES = boot_$(kernel_boot_arch).S kernel.c multiboot2.h
kernel_CCASFLAGS = $(kernel_ccasflags)
kernel_CFLAGS = $(kernel_cflags) -fno-builtin -nostdinc -O -g -Wall \
	-imacros $(top_builddir)/config.h
kernel_LDFLAGS = -nostdlib -Wl,-N -Wl,-Ttext -Wl,80100000 -Wl,--build-id=none

boot.o: multiboot2.h
endif

EXTRA_DIST = $(man_MANS) $(noinst_SCRIPTS) \
	$(EXAMPLES) $(multiboot_TEXINFOS)
CLEANFILES = $(noinst_PROGRAMS)

# Cancel the rule %.texi -> %. This rule may confuse make to determine
# the dependecies.
.texi:

%.c.texi: %.c $(srcdir)/$(SRC2TEXI)
	$(SHELL) $(srcdir)/$(SRC2TEXI) $(srcdir) $< $@

%.h.texi: %.h $(srcdir)/$(SRC2TEXI)
	$(SHELL) $(srcdir)/$(SRC2TEXI) $(srcdir) $< $@

%.S.texi: %.S $(srcdir)/$(SRC2TEXI)
	$(SHELL) $(srcdir)/$(SRC2TEXI) $(srcdir) $< $@
