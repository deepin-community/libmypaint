# Optional
if ENABLE_GEGL

AM_CPPFLAGS = \
	-I$(top_builddir) \
	-I$(top_srcdir)

## GObject introspection ##

-include $(INTROSPECTION_MAKEFILE)
INTROSPECTION_GIRS =
INTROSPECTION_SCANNER_ARGS = \
    --warn-all \
    --pkg="gegl-@GEGL_VERSION@" \
    --pkg="glib-2.0" \
    --namespace="MyPaintGegl" \
    --nsversion="$(LIBMYPAINT_MAJOR_VERSION).$(LIBMYPAINT_MINOR_VERSION)" \
    --identifier-prefix="MyPaintGegl" --symbol-prefix="mypaint_gegl" \
    --add-include-path="$(srcdir)/.." \
    --add-include-path="$(srcdir)" \
    --add-include-path="$(builddir)/.." \
    --add-include-path="`$(PKG_CONFIG) --define-variable=datadir="$(datadir)" --variable=girdir gobject-introspection-1.0`"
INTROSPECTION_COMPILER_ARGS = --includedir="$(srcdir)" \
     --includedir="$(srcdir)/.." \
     --includedir="$(builddir)/.." \
     --includedir="`$(PKG_CONFIG) --define-variable=datadir="$(datadir)" --variable=girdir gobject-introspection-1.0`"
INTROSPECTION_SCANNER_ENV = CFLAGS="$(CFLAGS)" LDFLAGS="$(LDFLAGS) -lm" CPPFLAGS="$(CPPFLAGS)" CXXFLAGS="$(CXXFLAGS)"

libmypaint_gegl_introspectable_headers = \
	../glib/mypaint-gegl-glib.h		\
	mypaint-gegl-surface.h

if HAVE_INTROSPECTION

introspection_sources = \
	$(libmypaint_gegl_introspectable_headers)	\
	../glib/mypaint-gegl-glib.c	\
	mypaint-gegl-surface.c

MyPaintGegl-@LIBMYPAINT_MAJOR_VERSION@.@LIBMYPAINT_MINOR_VERSION@.gir: libmypaint-gegl.la Makefile
MyPaintGegl_@LIBMYPAINT_MAJOR_VERSION@_@LIBMYPAINT_MINOR_VERSION@_gir_INCLUDES = GObject-2.0 MyPaint-$(LIBMYPAINT_MAJOR_VERSION).$(LIBMYPAINT_MINOR_VERSION) Gegl-@GEGL_VERSION@
MyPaintGegl_@LIBMYPAINT_MAJOR_VERSION@_@LIBMYPAINT_MINOR_VERSION@_gir_CFLAGS = $(AM_CFLAGS) $(AM_CPPFLAGS) -I. -I..
MyPaintGegl_@LIBMYPAINT_MAJOR_VERSION@_@LIBMYPAINT_MINOR_VERSION@_gir_LIBS = libmypaint-gegl.la ../libmypaint.la
MyPaintGegl_@LIBMYPAINT_MAJOR_VERSION@_@LIBMYPAINT_MINOR_VERSION@_gir_FILES = $(introspection_sources)
INTROSPECTION_GIRS += MyPaintGegl-@LIBMYPAINT_MAJOR_VERSION@.@LIBMYPAINT_MINOR_VERSION@.gir

girdir = $(datadir)/gir-1.0
gir_DATA = $(INTROSPECTION_GIRS)

typelibdir = $(libdir)/girepository-1.0
typelib_DATA = $(INTROSPECTION_GIRS:.gir=.typelib)

CLEANFILES = $(gir_DATA) $(typelib_DATA)

endif # HAVE_INTROSPECTION

## pkg-config file ##
pkgconfigdir = $(libdir)/pkgconfig
pkgconfig_DATA = libmypaint-gegl.pc

## libmypaint-gegl ##
lib_LTLIBRARIES = libmypaint-gegl.la

libmypaint_gegl_publicdir = $(includedir)/libmypaint-gegl

libmypaint_gegl_public_HEADERS = \
	$(libmypaint_gegl_introspectable_headers)

LIBMYPAINT_GEGL_SOURCES = \
	../glib/mypaint-gegl-glib.c	\
	mypaint-gegl-surface.c

libmypaint_gegl_la_SOURCES = $(libmypaint_gegl_public_HEADERS) $(LIBMYPAINT_GEGL_SOURCES)

libmypaint_gegl_la_CFLAGS = $(JSON_CFLAGS) $(GLIB_CFLAGS) $(GEGL_CFLAGS)
libmypaint_gegl_la_LIBADD = $(top_builddir)/libmypaint.la $(GEGL_LIBS)

endif # enable_gegl
