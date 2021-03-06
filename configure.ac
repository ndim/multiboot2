dnl Configure script for GRUB.
dnl Copyright 1999,2000,2001,2002,2003,2004,2005,2008,2009,2010 Free Software Foundation, Inc.

dnl Permission to use, copy, modify and distribute this software and its
dnl documentation is hereby granted, provided that both the copyright
dnl notice and this permission notice appear in all copies of the
dnl software, derivative works or modified versions, and any portions
dnl thereof, and that both notices appear in supporting documentation.
dnl
dnl THE FREE SOFTWARE FOUNDATION ALLOWS FREE USE OF THIS SOFTWARE IN ITS
dnl "AS IS" CONDITION.  THE FREE SOFTWARE FOUNDATION DISCLAIMS ANY
dnl LIABILITY OF ANY KIND FOR ANY DAMAGES WHATSOEVER RESULTING FROM THE
dnl USE OF THIS SOFTWARE.

AC_PREREQ(2.63)
AC_INIT([Multiboot], [2.0], [bug-grub@gnu.org])
AC_CONFIG_SRCDIR([doc/multiboot.texi])
AC_CONFIG_HEADER([config.h])
AM_INIT_AUTOMAKE

#
# Programs
#

AC_CHECK_TOOL(CC, gcc)
AC_PROG_CC
AM_PROG_AS
# We need this for older versions of Autoconf.
_AM_DEPENDENCIES(CC)

dnl Because recent automake complains about AS, set it here.
CCAS="$CC"
AC_SUBST(CCAS)

dnl Build the example Multiboot kernel (if possible on this host)
AC_CANONICAL_HOST
case "$host" in #(
  i[3456]86-*) kernel_boot_arch=i386
               ;; #(
  x86_64-*)    kernel_boot_arch=i386
               kernel_ccasflags="-m32"
               kernel_cflags="-m32"
	       ;; #(
  mips-*)      kernel_boot_arch=mips
               ;; #(
  *)           kernel_boot_arch=unsupported
               ;;
esac
AC_SUBST([kernel_boot_arch])
AC_SUBST([kernel_ccasflags])
AC_SUBST([kernel_cflags])

AC_ARG_ENABLE([example-kernel], [dnl
AS_HELP_STRING([--enable-example-kernel],
               [build the example Multiboot2 kernel])])

AM_CONDITIONAL([BUILD_EXAMPLE_KERNEL],
               [test "x$enable_example_kernel" = xyes && test "x$kernel_boot_arch" != "xunsupported"])

dnl Because recent automake complains about CCASFLAGS, set it here.
CCASFLAGS='$(DEFS) $(DEFAULT_INCLUDES) $(INCLUDES) $(CPPFLAGS) $(CFLAGS)'
AC_SUBST(CCASFLAGS)

CFLAGS="-nostdlib $CFLAGS"

dnl Output.
AC_CONFIG_FILES([Makefile doc/Makefile])
AC_OUTPUT
