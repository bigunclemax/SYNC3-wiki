
# Storage/FS subsystem
## Bootloader + Startup IFS

https://www.qnx.com/developers/docs/7.1/#com.qnx.doc.neutrino.building/topic/intro/intro_startup_sequence.html

`MLO` - ROM monitor or Multimedia card Loader.  
`Startup IFS` - Startup program, QNX kernel and rootfs

Layout on EMMC flash:
```
Block#    Offset in bytes          Name
---------------------------------------------------
0x0000    0x0000000                MBR
0x0002    0x0000400 (1024)         boot bank info
0x0100    0x0020000 (131072)       MLO
0x0184    0x0030800 (198656)       IFS first bank
0x7cd2    0x0F9A400 (16360448)     IFS second bank
```

## EMMC Partition table
```shell
# fdisk /dev/hd0 show -l

     _____OS_____     Start       End       ______Number______   Size    Boot  
     name    type     Block       Block     Cylinders   Blocks                 

1.   DOS        6          32       65535        32       65504     31 MB   *
2.   QNX6     177       65536     3211263      1536     3145728   1536 MB
3.   QNX6     178     3211264     6356991      1536     3145728   1536 MB
4.   Extd'd     5     6356992   122142719     56536   115785728  56536 MB
4.1  nonQNX   180     6357024   119595007     55292   113237984  55291 MB
4.2  BSD      181   119595040   122138623      1242     2543584   1241 MB
4.3  nonQNX   182   122138656   122142719         2        4064      1 MB
```

## hd0t180

Mountpoint: `/fs/images`

Called from startup script(startupIFS)  
```shell
mount -b -t qnx6 -o noatime,alignio /dev/hd0t180 /fs/images
```

## hd0t177 or hd0t178

Mountpoint: `/fs/mp`

Called from `/etc/script_mnt.sh` (startupIFS)
```shell
mmc_get_act /dev/hd0 0 > /tmp/mmcinfo
mount -b -r -t qnx6 -o snapshot=0,noatime,alignio $MMC_ACT_FS_PART /fs/mp
```

```shell
# cat /tmp/mmcinfo
MMC_ACT_FS_PART=/dev/hd0t177
MMC_PAS_FS_PART=/dev/hd0t178
MMC_ACT_IFS=0
MMC_PAS_IFS=1
ACT_IFS_ERROR=0
ACT_FS_ERROR=0
STARTUP_IFS_ERROR=0
```

## hd0t181

Mountpoint: `/fs/rwdata`

Called from startup script (startupIFS)  
```shell
mount -b -t qnx6 -o alignio /dev/hd0t181 /fs/rwdata &
```

## IFSs

Mountpoint: `/fs/mp/ifs`

Called from startup script
```shell
mount_ifs -b -f /fs/mp/ifs/renderer-ifs -m / &
mount_ifs -b -f /fs/mp/ifs/quickapps-ifs -m / &
mount_ifs -b -f /fs/mp/ifs/second-ifs -m / &
```
```shell
# use mount_ifs
mount_ifs mount-ifs Utility

Syntax: mount-ifs [-f filename][-m mountpoint]

Options:
   -f filename         source ifs file name
   -m 			mount point
   -b			daemonize before the real transfer (default is after).
   -T 			create a separate thread to do the decompress in parallel.
```

## Mount images
Called from `sh /etc/mount_all_images.sh`

## Some info
```shell
# ls -la /fs/images/
total 41277473
drwxrwxr-x  5 root      root            4096 Jan 01  1970 .
drwxr-xr-t  2 root      root              10 Jan 01  1970 ..
drwx------  2 root      root            4096 Jan 01  1970 .boot
drwxrwxrwx  4 root      root            4096 Jan 01 00:10 ivsu_cache
drwxrwxrwx  2 root      root            4096 Jan 01 00:10 ivsu_installcache
-rw-rw-rw-  1 root      root      3351511040 Jan 01  1970 map_comn.img
-rw-rw-rw-  1 root      root      3456892928 Jan 01  1970 map_euc.img
-rw-rw-rw-  1 root      root      3985637376 Jan 01  1970 map_eue.img
-rw-rw-rw-  1 root      root      3018063872 Jan 01  1970 map_eus.img
-rw-rw-rw-  1 root      root      1243611136 Jan 01  1970 map_ext.img
-rw-rw-rw-  1 root      root        76283904 Jan 01  1970 station_logos.img
-rw-rw-rw-  1 root      root      2072248320 Jan 01  1970 voice.img
-rw-rw-rw-  1 root      root      3929800704 Jan 01  1970 voice_nav_eucpr.img
```

```shell
# df -h
/fs/rwdata/ppsp                0         0         0     100%  /ppsp           
/dev/blk/ram-0-allo         128M      1.2M      127M       1%  /fs/tmpfs/      
/fs/images/map_ext.         1.1G      1.1G      892K     100%  /fs/sd/MAP/     
/fs/images/map_eus.         2.8G      2.7G       14M     100%  /fs/sd/MAP/     
/fs/images/map_eue.         3.7G      3.6G       21M     100%  /fs/sd/MAP/     
/fs/images/map_euc.         3.2G      3.2G      5.7M     100%  /fs/sd/MAP/     
/fs/images/map_comn         3.1G      3.0G       24M     100%  /fs/sd/MAP/     
/fs/images/voice_na         3.6G      3.6G       35M     100%  /fs/Nuance/     
/fs/images/voice.im         1.9G      1.9G      8.4M     100%  /fs/Nuance/     
/dev/hd0t181                1.2G      849M      393M      69%  /fs/rwdata/     
/dev/diagscratch0            35M       30K       35M       1%  /fs/rwdata/quip/
/dev/diagevents0             90M       68K       90M       1%  /fs/rwdata/quip/
/dev/hd0t177                1.4G      1.3G      126M      92%  /fs/mp/         
/fs/images/station_          73M       72M      432K     100%  /fs/mp/resources
/dev/hd0t180                 54G       22G       32G      41%  /fs/images/     
/var/pps                       0         0         0     100%  /pps            
/dev/hd0                    1.9M      1.9M         0     100%  /dev/hd0t182    
/dev/hd0                    1.5G      1.5G         0     100%  /dev/hd0t178    
/dev/hd0                     32M       32M         0     100%  /dev/hd0t6      
/dev/hd0                     58G       58G         0     100%  
```

```shell
# mount
/fs/rwdata/ppsp on /ppsp type PPS 
/dev/blk/ram-0-alloc-0-tmp on /fs/tmpfs type tmp 
/fs/images/map_ext.img on /fs/sd/MAP type qnx6 
/fs/images/map_eus.img on /fs/sd/MAP type qnx6 
/fs/images/map_eue.img on /fs/sd/MAP type qnx6 
/fs/images/map_euc.img on /fs/sd/MAP type qnx6 
/fs/images/map_comn.img on /fs/sd/MAP type qnx6 
/fs/images/voice_nav_eucpr.img on /fs/Nuance type qnx6 
/fs/images/voice.img on /fs/Nuance type qnx6 
/dev/hd0t181 on /fs/rwdata type qnx6 
/dev/diagscratch0 on /fs/rwdata/quip/forensics type qnx4 
/dev/diagevents0 on /fs/rwdata/quip/events type qnx4 
/dev/hd0t177 on /fs/mp type qnx6 
/fs/images/station_logos.img on /fs/mp/resources/station_logo/Logo type qnx6 
/dev/hd0t180 on /fs/images type qnx6 
/var/pps on /pps type PPS 
```

## Commands 

```shell
mount -uw /fs/mp/ #remount to RW
```

```shell
/fs/rwdata/dev/remount_rw.sh
/fs/rwdata/dev/remount_ro.sh
```
