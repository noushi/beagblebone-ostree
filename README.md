# beagblebone-ostree

## considerations

1. [ ] ostree + special devices restore
1. [wip] uboot + ostree (boot process)
1. [wip] custom beaglebone uboot compatibility w/ ostree
1. [ ] ostree kernel cmline argument value
1. [x] u-boot aware ostree layout

## diags on running system (no ostree)

### mount 
```
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=225192k,nr_inodes=56298,mode=755)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,noexec,relatime,size=50452k,mode=755)
/dev/mmcblk1p1 on / type ext4 (rw,noatime,errors=remount-ro)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
cgroup on /sys/fs/cgroup/systemd type cgroup (rw,nosuid,nodev,noexec,relatime,xattr,release_agent=/lib/systemd/systemd-cgroups-agent,name=systemd)
cgroup on /sys/fs/cgroup/net_cls,net_prio type cgroup (rw,nosuid,nodev,noexec,relatime,net_cls,net_prio)
cgroup on /sys/fs/cgroup/cpu,cpuacct type cgroup (rw,nosuid,nodev,noexec,relatime,cpu,cpuacct)
cgroup on /sys/fs/cgroup/perf_event type cgroup (rw,nosuid,nodev,noexec,relatime,perf_event)
cgroup on /sys/fs/cgroup/pids type cgroup (rw,nosuid,nodev,noexec,relatime,pids)
cgroup on /sys/fs/cgroup/freezer type cgroup (rw,nosuid,nodev,noexec,relatime,freezer)
cgroup on /sys/fs/cgroup/devices type cgroup (rw,nosuid,nodev,noexec,relatime,devices)
cgroup on /sys/fs/cgroup/blkio type cgroup (rw,nosuid,nodev,noexec,relatime,blkio)
cgroup on /sys/fs/cgroup/memory type cgroup (rw,nosuid,nodev,noexec,relatime,memory)
systemd-1 on /proc/sys/fs/binfmt_misc type autofs (rw,relatime,fd=30,pgrp=1,timeout=0,minproto=5,maxproto=5,direct,pipe_ino=13318)
debugfs on /sys/kernel/debug type debugfs (rw,relatime)
mqueue on /dev/mqueue type mqueue (rw,relatime)
configfs on /sys/kernel/config type configfs (rw,relatime)
fusectl on /sys/fs/fuse/connections type fusectl (rw,relatime)
tmpfs on /run/user/1000 type tmpfs (rw,nosuid,nodev,relatime,size=50448k,mode=700,uid=1000,gid=1000)
```

### find /boot

```
/boot
/boot/uboot
/boot/System.map-4.19.59-bone-rt-r36
/boot/uEnv.txt
/boot/vmlinuz-4.19.59-bone-rt-r36
/boot/SOC.sh
/boot/initrd.img-4.19.59-bone-rt-r36
/boot/config-4.19.59-bone-rt-r36
/boot/dtbs
/boot/dtbs/4.19.59-bone-rt-r36
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-wireless.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-evm.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-cm-t335.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-baltos-ir5221.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-baltos-ir3220.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblue.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-bonegreen-wireless.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-lxm.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-sbc-t335.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-bbb-exp-r.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-wl1835mod.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-nano.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-pdu001.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-bonegreen-wireless-uboot-univ.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-sancloud-bbe.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-phycore-rdk.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-baltos-ir2110.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-bbbmini.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-evmsk.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-bonegreen.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-abbbi.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-base0033.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-pepper.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-moxa-uc-8100-me-t.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-uboot.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-bone.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-icev2.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-shc.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-audio.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-pocketbeagle.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-bone-uboot-univ.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-wega-rdk.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-sl50.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-uboot-univ.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-chiliboard.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-osd3358-sm-red.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack.dtb
/boot/dtbs/4.19.59-bone-rt-r36/am335x-boneblack-bbb-exp-c.dtb
```


###  /boot/uEnv.txt

```
#Docs: http://elinux.org/Beagleboard:U-boot_partitioning_layout_2.0

uname_r=4.19.59-bone-rt-r36
#uuid=
#dtb=

###U-Boot Overlays###
###Documentation: http://elinux.org/Beagleboard:BeagleBoneBlack_Debian#U-Boot_Overlays
###Master Enable
enable_uboot_overlays=1

###Overide capes with eeprom
#uboot_overlay_addr0=/lib/firmware/.dtbo
#uboot_overlay_addr1=/lib/firmware/.dtbo
#uboot_overlay_addr2=/lib/firmware/.dtbo
#uboot_overlay_addr3=/lib/firmware/.dtbo

###Additional custom capes
#uboot_overlay_addr4=/lib/firmware/.dtbo
#uboot_overlay_addr5=/lib/firmware/.dtbo
#uboot_overlay_addr6=/lib/firmware/.dtbo
#uboot_overlay_addr7=/lib/firmware/.dtbo

###Custom Cape
#dtb_overlay=/lib/firmware/.dtbo

###Disable auto loading of virtual capes (emmc/video/wireless/adc)
#disable_uboot_overlay_emmc=1
#disable_uboot_overlay_video=1
disable_uboot_overlay_audio=1
#disable_uboot_overlay_wireless=1
#disable_uboot_overlay_adc=1

###PRUSS OPTIONS
###pru_rproc (4.4.x-ti kernel)
#uboot_overlay_pru=/lib/firmware/AM335X-PRU-RPROC-4-4-TI-00A0.dtbo
###pru_rproc (4.14.x-ti kernel)
#uboot_overlay_pru=/lib/firmware/AM335X-PRU-RPROC-4-14-TI-00A0.dtbo
###pru_rproc (4.19.x-ti kernel)
#uboot_overlay_pru=/lib/firmware/AM335X-PRU-RPROC-4-19-TI-00A0.dtbo
###pru_uio (4.4.x-ti, 4.14.x-ti, 4.19.x-ti & mainline/bone kernel)
uboot_overlay_pru=/lib/firmware/AM335X-PRU-UIO-00A0.dtbo

###Cape Universal Enable
enable_uboot_cape_universal=1

###Debug: disable uboot autoload of Cape
#disable_uboot_overlay_addr0=1
#disable_uboot_overlay_addr1=1
#disable_uboot_overlay_addr2=1
#disable_uboot_overlay_addr3=1

###U-Boot fdt tweaks... (60000 = 384KB)
#uboot_fdt_buffer=0x60000
###U-Boot Overlays###

cmdline=coherent_pool=1M net.ifnames=0 rng_core.default_quality=100 quiet
```
