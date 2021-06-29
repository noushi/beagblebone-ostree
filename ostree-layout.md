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

Symlinks to have:
| source | target |
|--|--|
| /boot/uEnv.txt | /boot/loader/uEnv.txt |
| /boot/loader   | /boot/loader.0  | 
| /boot/loader.0/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.0/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.0/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.0/config-current | /boot/loader.0/config-$version |

loader.0/
   |-> vmlinuz.0
   |-> initrd.0
   |-> grub.cfg
|-> loader.1/
   |-> vmlinuz.1
   |-> initrd.1
   |-> grub.cfg
|-> loader/
