Xilinx DNNDK for ZynqMP-FPGA-Linux
====================================================================================

Overview
------------------------------------------------------------------------------------

### Introduction

This repository provides information for creating debian packages for running Xilinx DNNDK on ZynqMP-FPGA-Linux(Debian10).

 * https://github.com/Xilinx/Edge-AI-Platform-Tutorials
 * https://github.com/ikwzm/ZynqMP-FPGA-Linux


Install
------------------------------------------------------------------------------------

### Boot Ultra96 and login fpga or root user

### Download

```console
shell$ git clone https://github.com/ikwzm/ZynqMP-FPGA-DNNDK.git
shell$ cd ZynqMP-FPGA-DNNDK
```

### Install with xlnx-dnndk debian package

```console
shell$ sudo dpkg -i xlnx-dnndk_0.3.3-0_arm64.deb
```

### Install with xlnx-dpu-kernel-module debian package

```console
shell$ sudo dpkg -i xlnx-dpu-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb
```

Build 
------------------------------------------------------------------------------------

### Download

```console
shell$ git clone https://github.com/ikwzm/ZynqMP-FPGA-DNNDK.git
shell$ cd ZynqMP-FPGA-DNNDK
shell$ git clone https://github.com/Xilinx/Edge-AI-Platform-Tutorials
```

### Build dnndk

```console
shell$ cd xlnx-dnndk/
shell$ sudo debian/rules binary
     :
     :
     :
shell$ cd ..
shell$ file xlnx-dnndk_0.3.3-0_arm64.deb
xlnx-dnndk_0.3.3-0_arm64.deb: Debian binary package (format 2.0)
```

### Build dpu kernel module (self compile)

```console
shell$ cd xlnx-dpu-kmod/
shell$ sudo debian/rules binary
     :
     :
     :
shell$ cd ..
shell$ file xlnx-dpu-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb
xlnx-dpu-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb: Debian binary package (format 2.0)
```

### Build dpu kernel module (cross compile)

```console
shell$ cd xlnx-dpu-kmod/
shell$ sudo debian/rules arch=arm64 deb_arch=arm64 kernel_release=v2019.1-zynqmp-fpga kernel_src_dir=<path>/linux-xlnx-v2019.1-zynqmp-fpga binary
     :
     :
     :
shell$ cd ..
shell$ file xlnx-dpu-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb
xlnx-dpu-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb: Debian binary package (format 2.0)
```

