# Contents
## This branch contains:
- Build script and patches to build host kernel/module/app (CentOS 8.1/CentOS 7.x)
- Build scripts to build OS images for VCAC-A card (Ubuntu 18.04).

# Documents
Get the Release Notes and Software Installation guide for how to setup the VCAC-A card from links below:
- [Release Notes](https://github.com/OpenVisualCloud/VCAC-SW-Analytics/blob/release/VCAC-A/R5/VCAC-A/Documents/VCAC-Analytics-releasenotes-rev5-0.pdf) 
- [Software Installation Guide](https://github.com/OpenVisualCloud/VCAC-SW-Analytics/blob/release/VCAC-A/R5/VCAC-A/Documents/VCAC-Analytics-software-installation-guide-rev5-0.pdf)

# Building
### Note: 
> Detailed instruction is distributed via User Guide.

## Prerequisite
Before being able to build and run docker, you will need install docker on your system. Please use https://docs.docker.com/install  to install docker-ce.

## Actual build
### Build kernel and driver module for host:   
```
cd VCAC-SW/VCAC-A/Intel_Media_Analytics_Host/scripts/
./build.sh -o <centos7/centos8>
	         centos7: build kernel and module for CentOS7.4 or CentOS7.6
	         centos8: build kernel and module for CentOS8.1
```

If the docker images used for compiling have been generated in an earlier execution, user can save time required to build them again by the following executions:
```
./build.sh -s -o <centos7/centos8>
```
	
### Build system image to be loaded on VCAC-A card:
```
cd VCAC-SW/VCAC-A/Intel_Media_Analytics_Node/scripts/
run: vcad_build.sh -o <BASIC/FULL/EXTENDED>  <options>
	         BASIC: basic OS image only with modules
	         FULL: OS image with MSS/OpenVINO installed
	         EXTENDED: installed binaries provides interfaces to mircrobenchmark tool
```
	
Check more options via 'vcad_build.sh -h', and below are some examples:

- Skip downloading source code and dependencies, put the files under /PATH/TO/PACKAGE/cache, then pass "-c" flag:
```
vcad_build.sh -o <BASIC/FULL/EXTENDED>  -c
```

- If the docker images used for compiling have been generated in an earlier execution, user can save time required to build them again by the following executions:
```
vcad_build.sh -o <BASIC/FULL/EXTENDED>  -s
```

- The size of the vcad system image is set to 48GB by default. And the system image size is configurable through passing flag "-e" followed by the image size measured in GB
```
vcad_build.sh -o <BASIC/FULL/EXTENDED>  -e 24
```

### Opt-in/out DL Streamer installation in silent mode
DL (Deep Learning) Streamer (GStreamer* Video Analytics Plugin, GVA) is included in OpenVINO 2020.2. After start vcad_build.sh with option "-o FULL" or "-o EXTENDED", a message will pop up to opt-in/out DL Streamer while installing OpenVINO.   
Silent mode is also provided with option "--silent silent.cfg", e.g:
```
vcad_build.sh -o <FULL/EXTENDED> --silent silent.cfg
``` 
The DL streamer opt-in/out is controlled by "GVA_INSTALL" parameter in silent.cfg under Intel_Media_Analytics_Node/scripts/
 
# Contributing
Use GitHub's "issues" or "pull-request" features, or reach via e-mail directly developers: Zhao, Ping or Liu, Yi (for e-mail addresses, look in git log). 
# License
GNU GENERAL PUBLIC LICENSE version 2
