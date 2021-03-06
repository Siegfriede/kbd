#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.60)
AC_INIT(kbd, 1.15, gladkov.alexey@gmail.com)
AM_INIT_AUTOMAKE
AC_CONFIG_SRCDIR([src/showkey.c])
AC_CONFIG_HEADERS(config.h)

# Checks for programs.
AC_PROG_YACC
AC_PROG_CC
AM_PROG_CC_C_O
AC_PROG_LEX
AC_PROG_SED
AC_PROG_INSTALL
AC_PROG_LN_S
AC_PROG_MAKE_SET
AC_CANONICAL_HOST

# Checks for libraries.

# Checks for header files.
AC_HEADER_DIRENT
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([fcntl.h libintl.h locale.h memory.h stdlib.h string.h \
sys/file.h sys/ioctl.h termios.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_C_INLINE
AC_TYPE_SIZE_T
AC_STRUCT_TM
AC_TYPE_UID_T

# Checks for library functions.
AC_FUNC_CHOWN
AC_FUNC_CLOSEDIR_VOID
AC_FUNC_FORK
AC_PROG_GCC_TRADITIONAL
AC_FUNC_MALLOC
AC_FUNC_REALLOC
AC_FUNC_SETPGRP
AC_TYPE_SIGNAL
AC_FUNC_STAT
AC_CHECK_FUNCS([alarm memset setlocale strcasecmp strchr strdup strerror \
strspn strstr strtol strtoul])

case $host_cpu in
	m68*|sparc*) KEYCODES_PROGS=no ;;
	*)           KEYCODES_PROGS=yes ;;
esac
AM_CONDITIONAL(KEYCODES_PROGS, test "$KEYCODES_PROGS" = "yes")

case $host_cpu in
	i?86*) RESIZECONS_PROGS=yes ;;
	*)     RESIZECONS_PROGS=no ;;
esac
AM_CONDITIONAL(RESIZECONS_PROGS, test "$RESIZECONS_PROGS" = "yes")

AC_ARG_ENABLE(optional-progs,
	AS_HELP_STRING(--enable-optional-progs, [Build and install a optional programs]),
	[OPTIONAL_PROGS=$enableval],[OPTIONAL_PROGS=no])
AM_CONDITIONAL(OPTIONAL_PROGS, test "$OPTIONAL_PROGS" = "yes")

# For lib/nls.h: do we have <libintl.h> and gettext() ?
AC_ARG_ENABLE(nls, AS_HELP_STRING(--enable-nls, [NLS support]),
	[enable_nls=$enableval], [enable_nls=no])

if test "$enable_nls" = "yes"; then
	AC_DEFINE(ENABLE_NLS, 1, [Enable Native Language Support])
fi

# Does xgettext exist and take the option --foreign-user?
FOREIGN=
HAVE_XGETTEXT=no
if (test "$enable_nls" = "yes" && type xgettext > /dev/null 2>&1); then
	msg=`xgettext --foreign-user 2>&1 | grep unrecognized`
	if test -z "$msg"; then
		FOREIGN="--foreign-user"
	fi
	HAVE_XGETTEXT=yes
fi
AC_SUBST(FOREIGN)
AC_SUBST(HAVE_XGETTEXT)

AC_CONFIG_FILES([Makefile
		data/Makefile
		man/Makefile
		man/man1/Makefile
		man/man1/dumpkeys.1
		man/man1/loadkeys.1
		man/man1misc/Makefile
		man/man5/Makefile
		man/man8/Makefile
		man/man8/loadunimap.8
		man/man8/mapscrn.8
		man/man8/setfont.8
		man/man8misc/Makefile
		po/Makefile
		src/Makefile])
AC_OUTPUT
