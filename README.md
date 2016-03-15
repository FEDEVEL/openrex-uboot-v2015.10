# About
This is a source code of uBoot v2015.10 for OpenRex board.

### About OpenRex
OpenRex is an open source hardware and software project.


Website: http://www.imx6rex.com/open-rex/

### More detailed software & hardware manual
For more detailed instructions about how to prepare software for OpenRex, go to:


http://www.imx6rex.com/open-rex/software/how-develop-your-own-software-uboot-linux-filesystem-yocto/

# Download source code
    git clone -b jethro https://github.com/FEDEVEL/openrex-uboot-v2015.10.git
    cd openrex-uboot-v2015.10

# Install & select cross compiler

### If you do not have any compiler installed (or you are not sure)
    apt-get install gcc-arm-linux-gnueabihf
    export CROSS_COMPILE=arm-linux-gnueabihf-

### If you have a compiler installed
    export CROSS_COMPILE=/opt/freescale/usr/local/gcc-4.6.2-glibc-2.13-linaro-multilib-2011.12/fsl-linaro-toolchain/bin/arm-none-linux-gnueabi-

# Setup Architecture
    export ARCH=arm

# Build 
Here are instructions how to compile the source code
### QUAD
    make distclean
    make mx6qopenrex_config
    make
    cp u-boot.imx /tftp/imx6/u-boot-imx6q-openrex.imx

### SOLO
    make distclean
    make mx6sopenrex_config
    make
    cp u-boot.imx /tftp/imx6/u-boot-imx6s-openrex.imx


# Update OpenRex uBoot
Go to OpenRex board, interrupt uBoot booting process (press any key). Then write following command:


    run update_spi_uboot

Note: if you would like to update SPI manually, you can use something like this:


    mw.b 0x10800000 0xFF 0x80000;tftp 0x10800000 imx6/u-boot-imx6q-openrex.imx;sf probe;sf erase 0x0 0x80000;sf write 0x10800000 0x400 0x80000

# Appendix
Here is a list of files, where we usually do changes:


    include/configs/mx6openrex.h
    include/configs/mx6openrex_common.h
    board/fedevel/mx6openrex/mx6openrex.c
    


