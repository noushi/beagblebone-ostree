# ostree layout (draft)

## os without ostree 

with /boot/uEnv.txt containing:
```
...
uname_r=$version
...
cmdline=coherent_pool=1M net.ifnames=0 lpj=1990656 rng_core.default_quality=100 quiet
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
| #TOP LEVEL SYMLINKS  |
| /boot/uEnv.txt | /boot/loader/uEnv.txt |
| /boot/loader/uEnv.txt | /boot/loader.0/uEnv.txt |
| /boot/System-map-current | /boot/loader/System-map-current |
| /boot/vmlinuz-current | /boot/loader/vmlinuz-current |
| /boot/initrd.img-current | /boot/loader/initrd.img-current |
| /boot/config-current | /boot/loader/config-current |
| | 
| # THE ATOMIC SWITCH |
| /boot/loader   | /boot/loader.0  | 
| | 
| # DEPLOYMENT 0 SYMLINKS |
| /boot/loader.0/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.0/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.0/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.0/config-current | /boot/loader.0/config-$version |
| | 
| # DEPLOYMENT 1 SYMLINKS |
| /boot/loader.1/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.1/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.1/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.1/config-current | /boot/loader.0/config-$version |


### /boot layout

minimal symlinks
| source | target |
|--|--|
| # TOP LEVEL SYMLINKS |
| /boot/uEnv.txt | /boot/loader/uEnv.txt |
| /boot/System-map-current | /boot/loader/System-map-current |
| /boot/vmlinuz-current | /boot/loader/vmlinuz-current |
| /boot/initrd.img-current | /boot/loader/initrd.img-current |
| /boot/config-current | /boot/loader/config-current |
| |
| # THE ATOMIC SWITCH |
| /boot/loader   | /boot/loader.0  | 
| |
| DEPLOYMENT 0 SYMLINKS |
| /boot/loader.0/System-map-current | /boot/loader.0/System-map-$version |
| /boot/loader.0/vmlinuz-current | /boot/loader.0/vmlinuz-$version |
| /boot/loader.0/initrd.img-current | /boot/loader.0/initrd.img-$version |
| /boot/loader.0/config-current | /boot/loader.0/config-$version |




### atomic switch

equivalent to:
```
ln -sf /boot/loader.$new /boot/loader
```

### uEnv.txt content

```
...
uname_r=current
...
cmdline=coherent_pool=1M net.ifnames=0 lpj=1990656 rng_core.default_quality=100 quiet $ostree_args
```

with:
```
ostree_args="ostree=/path/to/ostree/dir..."
```
