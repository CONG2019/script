# Scripts 

 A scripts repository that provides some docker build scripts for ARM. 

\* [Scripts](#scripts) 
  \* [Docker env](#docker-env) 
    \* [build_uboot](#build_uboot) 
    \* [build_arm](#build_arm)

## Docker env

> Providing some scripts that help for use docker images

### build_uboot

`build_uboot` is a docker build script that build uboot for rpi-zero.

1. Download `uboot` source code
```shell
git clone https://github.com/u-boot/u-boot.git
```
2. Download `docker_build` script
```shell
git clone https://github.com/CONG2019/script.git
```
3. Copy `build_uboot` script to uboot's root directory and entering uboot root directory
```shell
cp script/docker_env/build_uboot uboot/; cd uboot
```
4. **Now you can build uboot through docker**
```shell
# You can build as flow.
# Every time you run a command, it will start a new container which takes some time.
./build_uboot make rpi_0_w_defconfig
./build_uboot make -j4

# Or you can start docker first and then run build command in docker
./build_uboot
make rpi_0_w_defconfig
make -j4
exit
```

### build_arm

`build_arm` is a docker build script use docker image `cong2021/armenv`. `cong/2021/armenv` provides some commonly used ARM's toolchains that build by `ct-ng`, You can use this image build your toolschain also.

1. Download `build_arm` script

```shell
git clone https://github.com/CONG2019/script.git
```

2. Copy `build_arm` script to your working directory

```shell
cp script/docker_env/build_arm your_work_dir; cd your_work_dir
```

3. Start with build_arm

```shell
# Download docker image
./build_arm -i

# Show help
./build_arm -h

# Check docker image is ok
./build_arm -m rpi0 "arm-linux-gcc -v"
gcc version 11.2.0 (crosstool-NG 1.25.0)

# Build hello world
./build_arm -m rpi0 'arm-linux-gcc main.c -o hello_world'

# Start docker first and then run command in docker
./build_arm -m rpi0 '/bin/bash'
run command
... ...
exit

# Build your toolchains
./build_arm '/bin/bash' # Start docker
ct-ng list-samples
ct-ng armv6-unknown-linux-gnueabihf
ct-ng menuconfig
ct-ng build
exit
```

