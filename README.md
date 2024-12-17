1，shift + @中断进入serial

2，设置好tftpserver，修改网卡ip地址192.168.1.2，运行tftp32.exe。检查tftp server运行在192.168.1.2。

3，刷入128M rootfs分区
   tftpboot mibib_ccbikai.bin
   flash 0:MIBIB
   saveenv

4，重启shift + @中断进入serial

5，用smeminfo看一下mibib已经生效

6，tftpboot ***.ubi(固件名称)

7，imxtract 0x44000000 ubi && flash rootfs && reset

8，设置启动参数
set boot3 "set mtdparts mtdparts=nand0:0x8000000@0x0(fs)"\
set boot4 "ubi part fs && ubi read 42000000 kernel"\
set setup1 "partname=1 && setenv bootargs ubi.mtd=rootfs '${args_common}'"\
set setup2 "partname=2 && setenv bootargs ubi.mtd=rootfs '${args_common}'"\
saveenv

9，reset
