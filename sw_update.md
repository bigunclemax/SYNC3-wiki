# Update process

### APP_SUM
```
/fs/mp/apps/APP_SUM
/fs/mp/apps/usr/lib/libNS_ExtractVerifyCore.so
```

### NS_ExtractVerify 
ℹ️ Present only in reformat OS
```shell
Usage: SS_HashSpeedTest <certificate File Path> <src file> <dst Dir Path> <Particular file name to be extracted [Optional]>
```

Example:
```shell
NS_ExtractVerify /fs/mp/usr/share/ford_prod_ca_certs.pem PU5T-14G386-BB_1690840002000.TAR.GZ ./
```

### Certificates path
```shell
/fs/mp/usr/share/FmcIVSUInternalProdPublicCerts.pem
/fs/mp/usr/share/ford_prod_ca_certs.pem
/fs/mp/usr/share/prod-sync-modenc-g3-a2.pem
/fs/mp/usr/share/www.cloud-sync.ford.com.pem
/fs/mp/etc/AppLink/prodappissuingcatls.pem
/fs/mp/etc/AppLink/prodapproottls.pem
```