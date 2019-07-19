# jUboot
本项目基于u-boot2019进行开发，完全支持jLabSDR无线电实验平台<br>

## 编译环境
1. 宿主机操作系统：建议Ubuntu 16.04及以上版本 <br>
2. 交叉编译器：arm-linux-gnueabihf-gcc，<br>
   交叉编译器版本：6.5.0 (Linaro GCC 6.5-2018.12) ；<br>

## 编译步骤
1. export PATH="/home/armtool/gcc-linaro-6.5.0-2018.12-i686_arm-linux-gnueabihf/bin:$PATH"  #注意修改成当前系统编译器所在路径 <br>
2. export ARCH=arm<br>
3. export CROSS_COMPILE=arm-linux-gnueabihf-<br>
4. make   zynq_jLab_defconfig<br>
5. make<br>

## 引导内核
### 基本命令行参数设置<br>
* setenv bootargs=console=ttyPS0,115200 earlyprintk root=/dev/mmcblk0p2 rw * rootwait uio_pdrv_genirq.of_id=generic-uio  #SD卡启动根文件系统<br>
* bootargs=console=ttyPS0,115200 earlyprintk root=/dev/nfs nfsroot=192.168.15.10:/home/ubuntu_core_rootfs,tcp nolock ip=192.168.15.11:192.168.15.10:192.168.15.1:255.255.255.0:jf315:eth0:off rw uio_pdrv_genirq.of_id=generic-uio#TFTP服务器启动根文件系统<br>
* setenv ipaddr=0.0.0.0     #设置自身IP地址<br>
* setenv serverip=0.0.0.0   #设置服务器IP地址<br>
* setenv netmask=0.0.0.0    #设置mask<br>
* setenv bootdelay=4        #启动延时<br>
### 从SD卡启动

* uenvcmd=load mmc 0 0x2000000 uImage;load mmc 0 0x1f00000 zynq-zc702.dtb;bootm 0x2000000 - 0x1f00000<br>

### 从TFTP服务器启动 
* uenvcmd=tftpboot 0x2000000 uImage;tftpboot 0x1f00000 zynq-zc702.dtb;bootm 0x2000000 - 0x1f00000 <br>

### FIT格式镜像启动
* FIT格式镜像直接放到TFTP目录或者SD卡即可启动，制作方式参考[FIT文件制作](https://blog.csdn.net/qq_32938605/article/details/96479459) <br>

## 运行环境
jLab实验平台 1.0<br>
![load picture failed](https://github.com/JFounderSDR/openSCA/blob/master/jLab%E5%AE%9E%E9%AA%8C%E5%B9%B3%E5%8F%B0.png)<br>


如对上述项目有疑问，可发邮件至yhl@onetek.net进行咨询。
