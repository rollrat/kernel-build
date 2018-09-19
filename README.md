# kernel-build
How to build your own kernel

## Config-Build

```
$ make config
$ make menuconfig (need ncures)
$ make gconfig (need gtk+ gui)
$ make defconfig
```

```
$ zcat /proc/config.gz > .config
$ make oldconfig
```

```
$ make > /dev/null
```