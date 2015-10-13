AM_CPPFLAGS = @VMOD_INCLUDES@ -Wall -Werror

vmoddir = @VMOD_DIR@
vmod_LTLIBRARIES = libvmod_ofmTools.la

libvmod_ofmTools_la_LDFLAGS = -module -export-dynamic -avoid-version -shared

libvmod_ofmTools_la_SOURCES = \
	vmod_ofmTools.c

nodist_libvmod_ofmTools_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

vmod_ofmTools.lo: vcc_if.c vcc_if.h

vcc_if.c: vcc_if.h

vcc_if.h: @VMODTOOL@ $(top_srcdir)/src/vmod_ofmTools.vcc
	@VMODTOOL@ $(top_srcdir)/src/vmod_ofmTools.vcc

VMOD_TESTS = $(top_srcdir)/src/tests/*.vtc
.PHONY: $(VMOD_TESTS)

$(top_srcdir)/src/tests/*.vtc: libvmod_ofmTools.la
	@VARNISHTEST@ -Dvarnishd=@VARNISHD@ -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_ofmTools.vcc \
	$(VMOD_TESTS)

CLEANFILES = \
	$(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_ofmTools.rst \
	$(builddir)/vmod_ofmTools.man.rst
