# ostree layout (draft)

## os without ostree 

with /boot/uEnv.txt containing:
```
...
uname_r=$version
...
```

u-boot will bootstrap $version using the following files:
```
/boot/uEnv.txt
/boot/System-map-$version
/boot/vmlinuz-$version
/boot/initrd.img-$version
/boot/config-$version
```


## os with ostree

### /boot

