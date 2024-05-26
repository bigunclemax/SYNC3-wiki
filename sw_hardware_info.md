# General info
### QNX tools
#### `pidin`

https://china.qnx.com/developers/docs/6.4.1/neutrino/utilities/p/pidin.html

Display information about the system:

```shell
# pidin info
CPU:ARM Release:6.5.0  FreeMem:683Mb/2032Mb BootTime:Mar 19 17:35:42 UTC 2023
Processes: 139, Threads: 644
Processor1: 1093648626 Cortex A15 1000MHz FPU
Processor2: 1093648626 Cortex A15 1000MHz FPU
```

#### `uname`

https://china.qnx.com/developers/docs/6.4.1/neutrino/utilities/u/uname.html

Return the name of the operating system (POSIX):
```shell
# uname -a
QNX localhost 6.5.0 2019/12/12-16:00:38CST TI-OMAP5432-Pasa-Ford-Sync3 armle
```

### PASA tools
#### `hwid`

Displays info about S3 board.  
`hwid bt` - info about BT stack

```shell
# hwid
MY=17
RADIO_TYPE=NAVI
NVRAM_SIZE=64GB
RAM_SIZE=2GB
DRVC=0
CPU_FREQ=1000
HW_REVISION=A
```
