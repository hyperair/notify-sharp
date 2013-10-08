AC_INIT(src/Global.cs)

AC_CANONICAL_SYSTEM
AC_PREREQ(2.13)

API_VERSION=0.4
VERSION=$API_VERSION.1

AC_SUBST(API_VERSION)
AC_SUBST(VERSION)

AM_INIT_AUTOMAKE(notify-sharp, $VERSION)

AM_MAINTAINER_MODE

AC_PROG_INSTALL

AC_PATH_PROG(PKG_CONFIG, pkg-config, no)
if test "x$PKG_CONFIG" = "xno"; then
	AC_MSG_ERROR([You need to install pkg-config])
fi
AC_SUBST(PKG_CONFIG)

MONO_REQ_VERSION=1.1.13
PKG_CHECK_MODULES(MONO, mono >= $MONO_REQ_VERSION)

AC_PATH_PROG(GMCS, gmcs, no)
if test "x$GMCS" = "xno"; then
	AC_MSG_ERROR([You need to install gmcs])
fi
AC_SUBST(GMCS)

AC_PATH_PROG(GACUTIL, gacutil, no)
if test "x$GACUTIL" = "xno"; then
	AC_MSG_ERROR([You need to install gacutil])
fi
AC_SUBST(GACUTIL)

AC_ARG_ENABLE(docs, AC_HELP_STRING([--disable-docs], 
	[Do not build documentation]), with_docs=no, with_docs=yes)

MONODOC_REQ_VERSION=1.1.18

if test "x$with_docs" = "xyes"; then
	PKG_CHECK_MODULES(MONODOC, monodoc >= $MONODOC_REQ_VERSION,,
		[AC_MSG_ERROR([You need to install monodoc, or pass --disable-docs to configure to skip documentation installation])])
	AC_PATH_PROG(MONODOCER, monodocer, no)
	if test "x$MONODOCER" = "xno"; then
		AC_MSG_ERROR([You need to install monodoc, or pass --disable-docs to configure to skip documentation installation])
	fi
	
	AC_PATH_PROG(MDASSEMBLER, mdassembler, no)
	if test "x$MDASSEMBLER" = "xno"; then
		AC_MSG_ERROR([You need to install mdassembler, or pass --disable-docs to configure to skip documentation installation])
	fi
	
	DOCDIR=`$PKG_CONFIG monodoc --variable=sourcesdir`
	AC_SUBST(DOCDIR)
	AM_CONDITIONAL(BUILD_DOCS, true)
else
	AC_MSG_NOTICE([not building notify-sharp API documentation])
	AM_CONDITIONAL(BUILD_DOCS, false)
fi

GTK_SHARP_REQ_VERSION=2.99.1
PKG_CHECK_MODULES(GTK_SHARP, gtk-sharp-3.0 >= $GTK_SHARP_REQ_VERSION)
AC_SUBST(GTK_SHARP_LIBS)

DBUS_SHARP_REQ_VERSION=0.7
DBUS_SHARP_GLIB_REQ_VERSION=0.5
PKG_CHECK_MODULES(DBUS_SHARP, dbus-sharp-1.0 >= $DBUS_SHARP_REQ_VERSION \
                              dbus-sharp-glib-1.0 >= $DBUS_SHARP_GLIB_REQ_VERSION)
AC_SUBST(DBUS_SHARP_LIBS)

required_assemblies="Mono.Posix"

for asm in $required_assemblies; do
	AC_MSG_CHECKING([for $asm.dll])
	if test -n "`$GACUTIL /l $asm.dll | grep ^$asm.dll`"; then
		AC_MSG_RESULT([not found])
		AC_MSG_ERROR([missing required assembly in the GAC: $asm.dll])
	else
		AC_MSG_RESULT([found])
	fi
done

AC_OUTPUT([
Makefile
notify-sharp.pc
src/Makefile
src/AssemblyInfo.cs
docs/Makefile
])

