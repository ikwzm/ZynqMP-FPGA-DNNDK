prefix         ?= 
kernel_release ?= $(shell uname -r)
arch           ?= $(shell uname -m | sed -e s/arm.*/arm/ -e s/aarch64.*/arm64/)
host_arch      ?= $(shell uname -m | sed -e s/arm.*/arm/ -e s/aarch64.*/arm64/)
lib_dir        ?= $(prefix)/lib/modules/$(kernel_release)/xilinx
kernel_src_dir ?= /lib/modules/$(kernel_release)/build

curr_dir       ?= $(shell pwd)
src_dir        ?= $(curr_dir)/../Edge-AI-Platform-Tutorials/docs/DPU-Integration/reference-files/files/recipes-modules/dpu/files

src_files      = Makefile  \
                 dpucore.c \
                 dpucore.h \
                 dpuext.c  \
                 dpuext.h  \
                 dpudef.h  \
                 COPYING   \
                 $(ENDLIST)
build_dir      = ./dpu

kmod_objects   += $(build_dir)/dpu.ko

ifeq ($(arch), arm64)
 ifneq ($(host_arch), arm64)
   cross_compile  ?= aarch64-linux-gnu-
 endif
endif

.PHONY: all install $(build_dir)

all: dpu
	cd $(build_dir) ; $(MAKE) ARCH=$(arch) DPU_TARGET=1.3 CROSS_COMPILE=$(cross_compile) KERNEL_SRC=$(kernel_src_dir) all   ; cd $(curr_dir)

clean:
	cd $(build_dir) ; $(MAKE) ARCH=$(arch) DPU_TARGET=1.3 CROSS_COMPILE=$(cross_compile) KERNEL_SRC=$(kernel_src_dir) clean ; cd $(curr_dir)
	rm -rf $(build_dir)

install: all
	install -d $(lib_dir)
	for ko in $(kmod_objects); do install -m 0644 $$ko $(lib_dir) ; done

$(build_dir): $(addprefix $(src_dir)/,$(src_files))
	install -d $(build_dir)
	cp $^ $(build_dir)

