### index
- [compact vdi](#compact-vdi)

### compact vdi
zero linux file system
```
$ dd if=/dev/zero of=./bigemptyfile bs=4096k; rm -rf ./bigemptyfile
```

then, user virtualbox utility to compact vdi
```
VBoxManage modifyhd --compact xxx.vdi
```


