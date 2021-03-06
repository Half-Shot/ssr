AC_INIT([simplescreenrecorder], [0.1.0], [maarten-baert@hotmail.com])
AC_CONFIG_SRCDIR([src/Main.cpp])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])

AM_INIT_AUTOMAKE([foreign subdir-objects -Wall -Werror])
AM_MAINTAINER_MODE
AM_PROG_AR

LT_INIT
AC_SUBST([LIBTOOL_DEPS])

AC_PROG_CC
AC_PROG_CXX
AC_PROG_SED
AC_PROG_INSTALL

AC_ARG_ENABLE([glinjectlib], AS_HELP_STRING([--disable-glinjectlib], [don't build the GLInject library]))
AC_ARG_ENABLE([ssrprogram], AS_HELP_STRING([--disable-ssrprogram], [don't build the SimpleScreenRecorder program]))
AM_CONDITIONAL([ENABLE_GLINJECTLIB], [test x"$enable_glinjectlib" != x"no"])
AM_CONDITIONAL([ENABLE_SSRPROGRAM], [test x"$enable_ssrprogram" != x"no"])

AM_COND_IF([ENABLE_SSRPROGRAM], [
	PKG_PROG_PKG_CONFIG
	PKG_CHECK_MODULES([QT4], [QtCore QtGui >= 4.7.0], [
		QT_PATH="$( eval $PKG_CONFIG --variable=exec_prefix QtCore )"
		AC_PATH_PROGS([MOC], [moc-qt4 moc], [moc], [$QT_PATH/bin])
		AC_PATH_PROGS([RCC], [rcc-qt4 rcc], [rcc], [$QT_PATH/bin])
		AC_PATH_PROGS([UIC], [uic-qt4 uic], [uic], [$QT_PATH/bin])
	], [
		AC_MSG_ERROR([Qt 4 not found])
	])
])

AC_CHECK_LIB([rt], [clock_gettime], [ ], [AC_MSG_ERROR([required library missing])])

AM_COND_IF([ENABLE_GLINJECTLIB], [
	AC_CHECK_HEADER([dlfcn.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([dl], [dlsym], [ ], [AC_MSG_ERROR([required library missing])])
])

AM_COND_IF([ENABLE_SSRPROGRAM], [
	AC_CHECK_HEADER([libavformat/avformat.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([avformat], [av_guess_format], [ ], [AC_MSG_ERROR([required library missing])])
	AC_CHECK_HEADER([libavcodec/avcodec.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([avcodec], [avcodec_find_encoder_by_name], [ ], [AC_MSG_ERROR([required library missing])])
	AC_CHECK_HEADER([libavutil/avutil.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_HEADER([libavutil/mathematics.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([avutil], [av_rescale_q], [ ], [AC_MSG_ERROR([required library missing])])
	AC_CHECK_HEADER([libswscale/swscale.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([swscale], [sws_scale], [ ], [AC_MSG_ERROR([required library missing])])
])

AC_CHECK_HEADER([X11/Xlib.h], [ ], [AC_MSG_ERROR([required header missing])])
AC_CHECK_HEADER([X11/Xutil.h], [ ], [AC_MSG_ERROR([required header missing])], [#include <X11/Xlib.h>])
AC_CHECK_LIB([X11], [XOpenDisplay], [ ], [AC_MSG_ERROR([required library missing])])
AC_CHECK_HEADER([X11/extensions/Xfixes.h], [ ], [AC_MSG_ERROR([required header missing])], [#include <X11/Xlib.h>])
AC_CHECK_LIB([Xfixes], [XFixesGetCursorImage], [ ], [AC_MSG_ERROR([required library missing])])
AM_COND_IF([ENABLE_SSRPROGRAM], [
	AC_CHECK_HEADER([X11/extensions/XShm.h], [ ], [AC_MSG_ERROR([required header missing])], [#include <X11/Xlib.h>])
	AC_CHECK_LIB([Xext], [XShmCreateImage], [ ], [AC_MSG_ERROR([required library missing])])
])

AM_COND_IF([ENABLE_SSRPROGRAM], [
	AC_CHECK_HEADER([alsa/asoundlib.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([asound], [snd_pcm_open], [ ], [AC_MSG_ERROR([required library missing])])
	AC_CHECK_HEADER([pulse/context.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([pulse], [pa_context_new], [ ], [AC_MSG_ERROR([required library missing])])
])

AM_COND_IF([ENABLE_GLINJECTLIB], [
	AC_CHECK_HEADER([GL/gl.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_HEADER([GL/glext.h], [ ], [AC_MSG_ERROR([required header missing])], [#include <GL/gl.h>])
	AC_CHECK_HEADER([GL/glx.h], [ ], [AC_MSG_ERROR([required header missing])], [#include <GL/gl.h>])
	AC_CHECK_LIB([GL], [glPushAttrib], [ ], [AC_MSG_ERROR([required library missing])])
	AC_CHECK_HEADER([GL/glu.h], [ ], [AC_MSG_ERROR([required header missing])])
	AC_CHECK_LIB([GLU], [gluErrorString], [ ], [AC_MSG_ERROR([required library missing])])
])

AC_CONFIG_HEADERS([config.h])
AC_CONFIG_FILES([Makefile data/Makefile glinject/Makefile src/Makefile])
AC_OUTPUT
