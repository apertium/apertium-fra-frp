AC_PREREQ(2.52)

AC_INIT([Apertium French-Arpitan], [1.1.0], [hectoralos@gmail.com], [apertium-fra-frp], [https://wiki.apertium.org/wiki/Apertium-fra-frp])
AM_INIT_AUTOMAKE
AC_PROG_AWK

PKG_CHECK_MODULES(APERTIUM, apertium >= 3.8.3)
PKG_CHECK_MODULES(LTTOOLBOX, lttoolbox >= 3.7.1)
PKG_CHECK_MODULES(CG3, cg3 >= 1.3.9)
PKG_CHECK_MODULES(APERTIUM_LEX_TOOLS, apertium-lex-tools >= 0.4.2)
PKG_CHECK_MODULES(APERTIUM_SEPARABLE, apertium-separable >= 0.6.1)

AC_PATH_PROGS(ZCAT, [gzcat zcat], [false])
AS_IF([test x$ZCAT = xfalse], [AC_MSG_ERROR([You don't have zcat nor gzcat installed])])

m4_ifdef([AP_CHECK_LING],[],[AC_MSG_ERROR([AP_CHECK_LING not defined, is apertium.m4 in ACLOCAL_PATH? See: https://wiki.apertium.org/wiki/Installation_troubleshooting])])

AP_CHECK_LING([1], [apertium-fra], [1.12.0])
AP_CHECK_LING([2], [apertium-frp], [1.1.0])

PKG_CHECK_MODULES(REGTEST, apertium-regtest >= 0.9.1, [],
                  [AC_MSG_WARN([Running tests requires apertium-regtest])])

AP_MKINCLUDE

AC_OUTPUT([Makefile])
