# How to work with small device

1. Download `build_arm` script

   ```shell
   git clone https://github.com/CONG2019/script.git
   ```

2. Copy `build_arm` script to your working directory

   ```shell
   cp script/docker_env/build_arm your_work_dir; cd your_work_dir
   ```

3. Start with `build_arm`

   ```shell
   # Download docker image
   ./build_arm -i
   
   # Show help
   ./build_arm -h
   
   # Check docker image is ok
   ./build_arm -m c51 "sdcc --version"                                                 
   ARGS=[ -m 'c51' -- 'sdcc --version']
   machine=c51
   Toolchains: sdcc stcgal packihx hex2bin stcflash
   SDCC : mcs51/z80/z180/r2k/r2ka/r3ka/sm83/tlcs90/ez80_z80/z80n/ds390/pic16/pic14/TININative/ds400/hc08/s08/stm8/pdk13/pdk14/pdk15/mos6502 TD- 4.2.14 #13911 (Linux)
   published under GNU General Public License (GPL)
   ```

4. Lighting LED

   ```shell
   # create led.c
   #include <8052.h>
   
   void inline delay(unsigned int xms) {
       unsigned int i, j;
       for (i = xms; i > 0; i--)
           for (j = 110; j > 0; j--);
   }
   
   void main() {
       while (1) {
           P1_0 = 1;
           delay(1000);
           P1_0 = 0;
           delay(500);
       }
   }
   
   # compile led.c
   sdcc -mmcs51 led.c
   
   # flash
   stcgal -P stc89 -b 115200 -D led.ihx -p /dev/ttyUSB1
   ```

   