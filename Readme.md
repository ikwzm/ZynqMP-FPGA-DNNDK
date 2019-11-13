Xilinx DNNDK for ZynqMP-FPGA-Linux
============================================================================

Overview
----------------------------------------------------------------------------

### Introduction

This repository provides information for creating debian packages for running Xilinx DNNDK on ZynqMP-FPGA-Linux(Debian10).

 * https://github.com/Xilinx/Edge-AI-Platform-Tutorials
 * https://github.com/ikwzm/ZynqMP-FPGA-Linux


Install
----------------------------------------------------------------------------

### Boot Ultra96 and login fpga or root user

### Download

```console
shell$ git clone https://github.com/ikwzm/ZynqMP-FPGA-DNNDK.git
shell$ cd ZynqMP-FPGA-DNNDK
```

### Install dnndk with debian package

```console
shell$ sudo dpkg -i xlnx-dnndk_0.3.3-0_arm64.deb
(Reading database ... 67725 files and directories currently installed.)
Preparing to unpack xlnx-dnndk_0.3.3-0_arm64.deb ...
Unpacking xlnx-dnndk (0.3.3-0) ...
Setting up xlnx-dnndk (0.3.3-0) ...
```

### Install dpu.ko with debian package

```console
shell$ sudo dpkg -i xlnx-dpu-4.19.0-xlnx-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb
Selecting previously unselected package xlnx-dpu-4.19.0-xlnx-v2019.1-zynqmp-fpga.
(Reading database ... 67744 files and directories currently installed.)
Preparing to unpack xlnx-dpu-4.19.0-xlnx-v2019.1-zynqmp-fpga_1.3.0-0_arm64.deb ...
Unpacking xlnx-dpu-4.19.0-xlnx-v2019.1-zynqmp-fpga (1.3.0-0) ...
Setting up xlnx-dpu-4.19.0-xlnx-v2019.1-zynqmp-fpga (1.3.0-0) ...
```

### Build dpu_core.bin

```console
shell$ cd xlnx-dpu-core-ultra96/
shell$ make
```

### Install dpu_core

```console
shell$ sudo ./dtbocfg.rb -i dpu --dts dpu_core.dts
[ 2885.300524] fpga_manager fpga0: writing dpu_core.bin to Xilinx ZynqMP FPGA Manager
[ 2885.460207] fclkcfg amba_pl@0:fclk0: driver installed.
[ 2885.465404] fclkcfg amba_pl@0:fclk0: device name    : fclk0
[ 2885.470990] fclkcfg amba_pl@0:fclk0: clock  name    : pl0_ref
[ 2885.476742] fclkcfg amba_pl@0:fclk0: clock  rate    : 99999999
[ 2885.482595] fclkcfg amba_pl@0:fclk0: clock  enabled : 1
[ 2885.487820] fclkcfg amba_pl@0:fclk0: remove rate    : 1000000
[ 2885.493569] fclkcfg amba_pl@0:fclk0: remove enable  : 0
[ 2885.499796] [DPU][4937]Found DPU signature addr = 0x8f000000 in device-tree
[ 2885.506781] [DPU][4937]Checking DPU signature at addr = 0x8ff00000, 
[ 2885.513202] [DPU][4937]DPU signature checking done!

shell$ dexplorer -w
[DPU IP Spec]
IP  Timestamp   : 2019-08-28 13:00:00
DPU Core Count  : 1

[DPU Core List]
DPU Core        : #0
DPU Enabled     : Yes
DPU Arch        : B1152F
DPU Target      : v1.4.0
DPU Freqency    : 325 MHz
DPU Features    : Avg-Pooling, LeakyReLU/ReLU6, Depthwise Conv
```

### Uninstall dpu_core

```console
shell$ sudo ./dtbocfg.rb -r dpu
```

Build Debian Packages
----------------------------------------------------------------------------

### Download

```console
shell$ git clone https://github.com/ikwzm/ZynqMP-FPGA-DNNDK.git
shell$ cd ZynqMP-FPGA-DNNDK
shell$ git clone https://github.com/Xilinx/Edge-AI-Platform-Tutorials
```

### Build dnndk debian package

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

### Build dpu kernel module debian packages (self compile)

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

### Build dpu kernel module debian package (cross compile)

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

