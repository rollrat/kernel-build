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

## Implementaions on arch-x86

### locking

```
spin_lock()
asm/qspinlock.h:virt_spin_lock
atomic read val
 -> fail -> relax cpu "nop; rep;"
 -> hit -> atomic cmpxchg with zero
    -> if zero -> exit spin_lock
```
