
# DRM/GPU

https://www.qnx.com/developers/docs/8.0/com.qnx.doc.screen/topic/manual/cscreen_config_intro.html

Screen configs:
```shell
# cd /usr/lib/graphics/omap5430ES2_0/
# ls -l *.conf
lrwxrwxrwx  1 root      root             47 Jan 01 07:09 graphics.conf -> /usr/lib/graphics/omap5430ES2_0/graphics_l.conf
-rwxr-xr-x  1 root      root           1132 Jul 07  2023 graphics_l.conf
-rwxr-xr-x  1 root      root           1518 Jul 07  2023 graphics_p.conf
```

Content of `omap5430ES2_0`
```shell
# ls -l /usr/lib/graphics/omap5430ES2_0/
-rwxr-xr-x  1 root      root           1132 Jul 07  2023 graphics_l.conf
-rwxr-xr-x  1 root      root           1518 Jul 07  2023 graphics_p.conf
-rwxr-xr-x  1 root      root         156128 Jul 07  2023 libGalcore.so
-rwxr-xr-x  1 root      root          80160 Jul 07  2023 libIMGegl.so
-rwxr-xr-x  1 root      root         622858 Jul 07  2023 libImgGLESv1_CM.so
-rwxr-xr-x  1 root      root         579327 Jul 07  2023 libImgGLESv2.so
-rwxr-xr-x  1 root      root          12918 Jul 07  2023 libPVRScopeServices.so
-rwxr-xr-x  1 root      root         238627 Jul 07  2023 libWFDomap5430ES2_0.so
-rwxr-xr-x  1 root      root         357126 Jul 07  2023 libglslcompiler.so
-rwxr-xr-x  1 root      root          28319 Jul 07  2023 libpvr2d.so
-rwxr-xr-x  1 root      root         260768 Jul 07  2023 libsrv_um.so
-rwxr-xr-x  1 root      root        1712821 Jul 07  2023 libusc.so
lrwxr-xr-x  1 root      root             14 Jul 07  2023 libwfdcfg-sync3.so -> libwfdcfg.so.0
-rwxr-xr-x  1 root      root          10922 Jul 07  2023 libwfdcfg.so.0
-rwxr-xr-x  1 root      root         259185 Jul 07  2023 pvrsrv.so
-rwxr-xr-x  1 root      root          91225 Jul 07  2023 pvrsrvinit.so
-rwxr-xr-x  1 root      root          26403 Jul 07  2023 wsegl-screen.so
```

```
NAME=libWFDomap5430ES2_0.so
DESCRIPTION=OpenWF Display for TI omap5430ES2_0
```
