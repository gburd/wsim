#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.

AC_PREREQ(2.59)
PACKAGE=dbsql
AC_INIT(Sail is a Wooden Ships and Iron Men command line game,
        __EDIT_SAIL_VERSION__,
        support@wsim.org,
        sail-__EDIT_SAIL_VERSION__)
AC_CONFIG_SRCDIR([../src/game.c])
AC_CONFIG_HEADERS([sail_config.h:config.hin])

# Configure setup.
AC_CANONICAL_HOST()
AC_ARG_PROGRAM()

# Check for programs used in building and installation.
AM_PROGRAMS_SET
AC_PROG_INSTALL

# Don't build in the top-level or dist directories.
AC_MSG_CHECKING(if building in the top-level or dist directories)
if [ test -d build_unix -o -d aclocal ] ; then
        AC_MSG_RESULT(yes)
        AC_MSG_ERROR(
    [Sail should not be built in the top-level or dist directories.])
fi
AC_MSG_RESULT(no)

# The default compiler is cc (NOT gcc), the default CFLAGS is as specified
# above, NOT what is set by AC_PROG_CC, as it won't set optimization flags
# for any compiler other than gcc.
AC_PROG_CC(cc gcc)

# Do some gcc specific configuration.
AC_GCC_CONFIG1
AC_GCC_CONFIG2

# Export our compiler preferences for the libtool configuration.
export CC CCC

# Checks for programs.
AC_PROG_CC

# Libtool configuration.
AC_PROG_LIBTOOL
LIBTOOL_PROG="${SHELL} ./libtool"
INSTALLER="\$(LIBTOOL) --mode=install cp -p"
MAKEFILE_CC="\$(LIBTOOL) --mode=compile ${MAKEFILE_CC}"
MAKEFILE_CCLINK="${CC}"
MAKEFILE_CCLINK="\$(LIBTOOL) --mode=link ${MAKEFILE_CCLINK}"
LIBTOOL="\$(SHELL) ./libtool"

# Checks for libraries.

# Checks for header files.
AC_HEADER_STDC
AC_HEADER_SYS_WAIT
AC_CHECK_HEADERS([fcntl.h stdlib.h string.h unistd.h])

# Checks for typedefs, structures, and compiler characteristics.
AC_C_CONST
AC_TYPE_SIZE_T

# Checks for library functions.
AC_FUNC_FORK
AC_TYPE_SIGNAL
AC_FUNC_STAT
AC_FUNC_VPRINTF
AC_FUNC_WAIT3
AC_CHECK_FUNCS([alarm strrchr])

# Substitution variables.
AC_SUBST(CFLAGS)
AC_SUBST(CPPFLAGS)
AC_SUBST(LIBTOOL)
AC_SUBST(MAKEFILE_CC)
AC_SUBST(MAKEFILE_CCLINK)
AC_SUBST(o)

# Configure for shared libraries, static libraries, or both.  If both are
# configured, build the utilities and example programs with shared versions.
#
# $o is set to ".o" or ".lo", and is the file suffix used in the Makefile
# instead of .o
if test `$LIBTOOL_PROG --config |
    grep build_libtool_libs | grep no` 2>/dev/null; then
	enable_shared="no"
else
	enable_shared="yes"
fi
if test `$LIBTOOL_PROG --config |
    grep build_old_libs | grep no` 2>/dev/null; then
	enable_static="no"
else
	enable_static="yes"
fi

# C API.
if test "$enable_shared" = "no"; then
	DEFAULT_LIB="\$(libdb_version)"
	POSTLINK=": "
	o=".o"
else
	DEFAULT_LIB="\$(libso_target)"
	POSTLINK="\$(LIBTOOL) --mode=execute true"
	o=".lo"
fi

# Create the sail.h file from a source file and a list of global function
# prototypes.
CREATE_LIST="Makefile
sail.h:$srcdir/../src/sail.in"

AC_CONFIG_FILES($CREATE_LIST)
AC_OUTPUT
