# uboot_env, providing a docker build shell for uboot
## How to start?
1. Download uboot source code
```shell
git clone https://github.com/u-boot/u-boot.git
```
2. Download my `docker_build` script
```shell
git clone git@github.com:CONG2019/uboot_env.git
```
3. Copy `docker_build` script to uboot's root directory and entering uboot root directory
```shell
cp uboot_env/docker_build uboot/; cd uboot
```
4. **Now you can build uboot through docker**
```shell
# You can build as flow.
# Every time you run a command, it will start a new container which takes some time.
./docker_build make rpi_0_w_defconfig
./docker_build make -j4

# Or you can start docker first and then run build command in docker
./docker_build
make rpi_0_w_defconfig
make -j4
exit
```
