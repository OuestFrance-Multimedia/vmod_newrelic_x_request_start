AM_CPPFLAGS = @VMOD_INCLUDES@ -Wall -Werror

vmoddir = @VMOD_DIR@
vmod_LTLIBRARIES = libvmod_newrelic_x_request_start.la

libvmod_newrelic_x_request_start_la_LDFLAGS = -module -export-dynamic -avoid-version -shared

libvmod_newrelic_x_request_start_la_SOURCES = \
	vmod_newrelic_x_request_start.c

nodist_libvmod_newrelic_x_request_start_la_SOURCES = \
	vcc_if.c \
	vcc_if.h

vmod_newrelic_x_request_start.lo: vcc_if.c vcc_if.h

vcc_if.c: vcc_if.h

vcc_if.h: @VMODTOOL@ $(top_srcdir)/src/vmod_newrelic_x_request_start.vcc
	@VMODTOOL@ $(top_srcdir)/src/vmod_newrelic_x_request_start.vcc

VMOD_TESTS = $(top_srcdir)/src/tests/*.vtc
.PHONY: $(VMOD_TESTS)

$(top_srcdir)/src/tests/*.vtc: libvmod_newrelic_x_request_start.la
	@VARNISHTEST@ -Dvarnishd=@VARNISHD@ -Dvmod_topbuild=$(abs_top_builddir) $@

check: $(VMOD_TESTS)

EXTRA_DIST = \
	vmod_newrelic_x_request_start.vcc \
	$(VMOD_TESTS)

CLEANFILES = \
	$(builddir)/vcc_if.c \
	$(builddir)/vcc_if.h \
	$(builddir)/vmod_newrelic_x_request_start.rst \
	$(builddir)/vmod_newrelic_x_request_start.man.rst
