prefix     ?= ./
curr_dir   ?= $(shell pwd)
srcdir     ?= $(curr_dir)/../Edge-AI-Platform-Tutorials/docs/DPU-Integration/reference-files/files/recipes-apps/dnndk/files
bindir     := $(prefix)/usr/bin
libdir     := $(prefix)/usr/lib
includedir := $(prefix)/usr/include/

.PHONY: install

clean:

all:

install: all
	install -d $(bindir)
	install -m 0755 $(srcdir)/bin/dexplorer         $(bindir)
	install -m 0755 $(srcdir)/bin/dsight            $(bindir)
	install -d $(includedir)/dnndk/
	install -m 0644 $(srcdir)/include/dnndk.h       $(includedir)/dnndk/
	install -m 0644 $(srcdir)/include/dputils.h     $(includedir)/dnndk/
	install -m 0644 $(srcdir)/include/n2cube.h      $(includedir)/dnndk/
	install -d $(libdir)
	install -m 0655 $(srcdir)/lib/echarts.js        $(libdir)
	install -m 0655 $(srcdir)/lib/libdputils.so.3.3 $(libdir)
	install -m 0655 $(srcdir)/lib/libdsight.a       $(libdir)
	install -m 0655 $(srcdir)/lib/libhineon.so	$(libdir)
	install -m 0655 $(srcdir)/lib/libn2cube.so	$(libdir)
	cd $(libdir) && ln -s libdputils.so.3.3 libdputils.so
	install -d $(prefix)/usr/local/lib
	cd $(prefix)/usr/local/lib && ln -s ../../lib/libn2cube.so libn2cube.so

