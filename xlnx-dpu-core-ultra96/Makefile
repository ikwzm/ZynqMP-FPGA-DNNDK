prefix         ?= 
curr_dir       ?= $(shell pwd)
src_dir        ?= $(curr_dir)/../Edge-AI-Platform-Tutorials/docs/DPU-Integration/reference-files/prebuilts
lib_dir        ?= $(prefix)/lib/firmware

.PHONY: all install

all: dpu_core.bin

clean:
	rm design_1_wrapper.bit dpu_core.bin

install: all
	install -d $(lib_dir)
	install -m 0644 dpu_core.bin $(lib_dir)

design_1_wrapper.bit : $(src_dir)/design_1_wrapper.hdf
	unzip -o $< $@

dpu_core.bin : dpu_core.bif design_1_wrapper.bit
	bootgen -arch zynqmp -image dpu_core.bif -w -o dpu_core.bin

