# stm32f103cxt6

## Problems with USB to UART PL2303

- Config putty to receive and transmitt data 
> Setting default will not receive and transmitt data to PL2303

<img src = image/pl2303_4.png width = "350" />

- Let setting below:

<img src = image/configPutty.png width = "350" />

- **Set Flow control : None**
- Parity : None
- Test result
<img src = image/pl2303_2.png width = "350" />
<img src = image/pl2303_3.png width = "350" />

# How to install arm-gcc to programming for stm32f103 and install st-flash

## 1. Install arm-none-eabi-gcc 
- Dowload tool version below: 

>gcc-arm-none-eabi-10.3-2021.10-x86_64-linux.tar.bz2

- Extract file and **cd gcc-arm/bin/** , run command below to check version:

>./arm-none-eabi-gcc -v

![Alt text](image/image.png)

- Note: Save path to change path arm-gcc in Makefile for projects:

> PREFIX = /home/chung/laptrinh/stm32/tool/gcc-arm/bin/arm-none-eabi-

# 2. Install st-flash for programming stm32
- Web: https://github.com/stlink-org/stlink/releases
- Now, Ubuntu version is a 18.04 so not download last version of stlink in web. Go to release and choose version 1.5.0

![Alt text](image/dv.jpg)

- Extract file using command below: 

>unzip stlink-1.5.0.zip -d [directory]

- Go to stlink-1.5.0/doc and review file compiling.md, that is tutorial install

> nano stlink-1.5.0/doc/compiling.md 

- In compiling.md file have note install libusb1.0 and fix error when compiling

```
# Compiling
## Build from sources
* CMake (minimal v2.8.7)
* C compiler (gcc, clang, mingw)
* Libusb 1.0 (minimal v1.0.9)
* (optional) pandoc for generating manpages from markdown
...
## Linux
## Common requirements
* Debian based distros (debian, ubuntu)
  * `build-essential`
* `cmake`
* `libusb-1.0` (plus development headers for building, on debian based distros $
* (optional) for `stlink-gui` we need libgtk-3-dev

### Fixing cannot open shared object file

When installing system-wide (`sudo make install`) the dynamic library cache needs to be updated with the command `ldconfig`.
```

- Note: install **libusb-1.0**
- Before run **sudo make** need run **sudo ldconfig** fot not error as below: 

> error while loading shared libraries: libstlink-shared.so.1

- After run **sudo make** go to build/Release :

```
$laptrinh/stm32/tool/stlink-1.5.0/build/Release$ ls
CMakeCache.txt           include                    src
CMakeFiles               libstlink.a                st-flash
cmake_install.cmake      libstlink-shared.so        st-info
CPackConfig.cmake        libstlink-shared.so.1      tests
CPackSourceConfig.cmake  libstlink-shared.so.1.5.0  usr
doc                      Makefile
```
- run command **./st-flash** and **./st-info** for check:

```
$/aptrinh/stm32/tool/stlink-1.5.0/build/Release$ ./st-info --version
v1.5.0

$laptrinh/stm32/tool/stlink-1.5.0/build/Release$ ./st-flash
invalid command line
stlinkv1 command line: ./st-flash [--debug] [--reset] [--format <format>] [--flash=<fsize>] {read|write} /dev/sgX <path> <addr> <size>
stlinkv1 command line: ./st-flash [--debug] /dev/sgX erase
stlinkv2 command line: ./st-flash [--debug] [--reset] [--serial <serial>] [--format <format>] [--flash=<fsize>] {read|write} <path> <addr> <size>
stlinkv2 command line: ./st-flash [--debug] [--serial <serial>] erase
stlinkv2 command line: ./st-flash [--debug] [--serial <serial>] reset
                       Use hex format for addr, <serial> and <size>.
                       fsize: Use decimal, octal or hex by prefix 0xXXX for hex, optionally followed by k=KB, or m=MB (eg. --flash=128k)
                       Format may be 'binary' (default) or 'ihex', although <addr> must be specified for binary format only.
                       ./st-flash [--version]
```

- For run command st-flash and st-info in everywhere need copy it to /usr/bin/:

> sudo cp st-flash /usr/bin
> sudo cp st-info /usr/bin

## Install openOCD and gdb-multiarch for debug stm32f103

- Install gdb-multiarch

![Alt text](image/gdb-mul.png)

- Install libtool

![Alt text](image/libtool.png)

- Install openOCD

![Alt text](image/openocd.png)
![Alt text](image/openocd_version.png)


## Link reference:
>   https://tapit.vn/chuc-nang-lowpower-mode-cua-mcu-stm32f103c8t6/ 
>   https://tapit.vn/real-time-clock-rtc-tren-stm32f103c8t6/

>   https://hocarm.org/gioi-thieu-mot-so-he-dieu-hanh-thoi-gian-thuc/
>   https://hocarm.org/tag/stm32/page/4/
>   https://hocarm.org/su-dung-swo-de-debug-thong-tin-tu-stm32/
>   https://hocarm.org/rtos-software-timer/
>   https://hocarm.org/rtos-co-ban-phan-1/

>   https://iot47.com/nhung-va-phat-am-thanh-tren-stm32-voi-dma-va-pwm/
>   https://iot47.com/nhung-va-phat-am-thanh-tren-stm32-voi-dma-va-pwm/

>   https://laptrinharmst.blogspot.com/2018/02/bai-00-gioi-thieu-ve-stm32f103c8$
>   https://laptrinharmst.blogspot.com/2018/04/bai-13-rtc-voi-stm32f103.html

>   https://elec2pcb.com/2023/12/12/stm32_hal_cubemx_gnu_make_pyocd/?fbclid=IwA$

>   https://solutionias.com/giao-tiep-can-la-gi-cau-truc-va-ung-dung/#:~:text=C$

### mpu6050 library:
>   https://stm32f4-discovery.net/download/tm_stm32f4_mpu6050/

### The STM32G030
>   https://ioprog.com/2020/05/03/the-stm32g030/

