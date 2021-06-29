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

### /boot symlinks

Notes: 
- deployment `0` is the current deployment
- some symlinks are redundant and just shown for illustration)

| source | target |
|--|--|
|#top level files  |
| /boot/uEnv.txt | /boot/loader/uEnv.txt |
| /boot/loader/uEnv.txt | /boot/loader.0/uEnv.txt |
| /boot/System-map-current | /boot/loader.0/System-map-current |
| /boot/vmlinuz-current | /boot/loader.0/vmlinuz-current |
| /boot/initrd.img-current | /boot/loader.0/initrd.img-current |
| /boot/config-current | /boot/loader.0/config-current |
| # ze switch  |
| /boot/loader   | /boot/loader.0  | 
| # deployment 0 files | 
| /boot/loader.0/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.0/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.0/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.0/config-current | /boot/loader.0/config-$version |
| # deployment 1 files | 
| /boot/loader.1/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.1/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.1/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.1/config-current | /boot/loader.0/config-$version |


### /boot layout

minimal symlinks
| source | target |
|--|--|
| /boot/uEnv.txt | /boot/loader/uEnv.txt |
| /boot/loader   | /boot/loader.0  | 
| /boot/loader/uEnv.txt | /boot/loader.0/uEnv.txt |
| /boot/loader.0/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.0/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.0/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.0/config-current | /boot/loader.0/config-$version |




### atomic switch

equivalent to:
```
ln -sf /boot/loader.$new /boot/loader
```

