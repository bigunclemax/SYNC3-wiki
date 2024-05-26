
# LOG subsystem

## QNX system logs
`/bin/sloginfo` - [print system log](https://openqnx.com/static/neutrino/utilities/s/sloginfo.html)  
`/proc/boot/slogger` - [system logger](https://openqnx.com/static/neutrino/utilities/s/slogger.html)

## PASA tools
### nslogutil

`/fs/mp/apps/usr/sbin/nslogutil`

```
Help: nslogutil -q QUEUENAME [-m MASKVALUE(hex)] | [-l "slogger|msgq|console"] [-p "log message"] [-s severity] [-g "mask|outopt|severity"] [-t "rxontxoff, rxofftxon, rxontxon, rxofftxoff"] [-d Debug Dump Request]
```

Examples:  
`nslogutil -q IPC_MID -l "slogger" -m 0xefffffff`  
`nslogutil -q IPC_MID -m 0xFFFFFF -t rxontxon -s 1`  

### CustomCommandLineOption()
S3 common cmdline options (`CustomCommandLineOption()`):

```
optstr: "l:m:t:c:p:qr:s"

-l (log output option)
    Allowed values: "slogger", "console", "shmem" (And always to fs/rwdata/fordlogs/)
    This vales may be combined with '|' Ex: -l "slogger|console"

-m (mask value) This log level masks(Up to 16 masks). Each mask represent certain subsystem.
                Ex: -m "0xFFFFFFFF,0xFFFFFFFF,0xFFFFFFFF,0xFFFFFFFF"

-r [plog output option (byte)] Enable PLOG
-s Enable sys event log
-q queue name <%s>
-p (set priority) <??? %s>
-c (set config file) <filepath %s>
-t (set transmit logging) <??? %s>
```

## Log paths
```shell
/fs/rwdata/fordlogs/pas_debug.log
/fs/rwdata/fordlogs/BTLogs/NET_BT_Service.log
/fs/rwdata/logs/sys_error.log.0
/fs/rwdata/logs/96.bmetrics_data.log
/fs/rwdata/logs/96.ns_perf.log
/fs/rwdata/slogs/96.slog
/fs/rwdata/logs/sys_slog_info
/fs/rwdata/NAV/gnss/96-MSL_Log.txt
/fs/rwdata/NAV/gnss/96-CL_Log.txt
/fs/rwdata/NAV/unifiedsearch.log
/fs/rwdata/BEZEL_DIAGNOSTICS_LOG.txt
/fs/mp/NAV/Job2/resource/config/log.xml
/fs/mp/etc/AppLink/log4cxx.debug.properties
/fs/mp/etc/AppLink/log4cxx.properties
/fs/mp/etc/BT_HCILogSize.cfg
/fs/mp/etc/firmware/NS_SLog_config.cfg
/fs/mp/diagnostics/etc/quip/log_silver_config
/fs/mp/diagnostics/scripts/filter-btlog.sed
/fs/mp/diagnostics/scripts/filter-nuancelog.sed
/fs/mp/diagnostics/scripts/filter-osapilog.sed
/fs/mp/diagnostics/scripts/filter-slog.sed
/fs/mp/diagnostics/scripts/quip-log-silver.sh
/fs/images/ivsu_cache/Encoded_Interrogator_Log.xml
/dev/shmem/fts_log1.tmp
/dev/shmem/osapi.log
/dev/shmem/animamtion.log
/dev/shmem/NavMiniApplog.txt
/dev/shmem/NavAccellog.txt
```

### Other
```shell
/usr/sbin/tracelogger
/apps/NS_PasLogCapture
/fs/mp/apps/RCN_DiagnosticsLog
/fs/mp/apps/SS_SLogMonitor
/fs/mp/apps/VCA_Logger_Enable

/proc/boot/libPlog.so.1
/fs/mp/apps/usr/lib/libArtLog.so
/fs/mp/apps/usr/lib/liblog4cxx.so.10
/fs/mp/apps/usr/lib/libNS_Logger.so
/fs/mp/apps/usr/lib/libresource_logger.so
/fs/mp/usr/lib/liblogging.so.1
/fs/mp/NAV/libclientlogger.so
/fs/mp/NAV/libNAV_TI_Log.so

/fs/mp/qt5/qml/QtTest/testlogger.js
/fs/mp/fordhmi/test/alsim_loglevelset
/fs/mp/fordhmi/test/HmiLogScript.sh
```
