# OS update package

**All commands and tools described here work on Linux**

### Top layer archive
```shell
$ tar -tf NU5T-14G381-AD_1689364279000.TAR.GZ

Version.der # Update certificate
apps.tar.gz # Apps partition
QNX-IFS     # StartupIFS
MLO         # Bootloader
```

### apps.tar.gz
```shell
$ tar -tf apps.tar.gz 

apps.img   # qnx6fs image for hd0t177 or hd0t178
```

This image can be mounted with:
```shell
$ mount -t qnx6,ro -o loop apps.img /mnt/
```

### QNX-IFS

Ifs images can be upacked and **repacked** with [mkxfs](https://github.com/bigunclemax/mkxfs)
```
$ dumpifs -xr QNX-IFS
```
