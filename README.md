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

## Configures

Debugging

 * http://static.lwn.net/images/pdf/LDD3/ch04.pdf
 * https://fedoraproject.org/wiki/KernelDebugStrategy
 * http://deathbytape.com/articles/2015/02/17/build-debug-linux-kernel.html

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

```
mutex_lock()
kernel/locking/mutex.c:__mutex_lock_common
mutex_trylock
 -> fail -> spin_lock(wait) -> try again
                                   -> fail -> make waiter -> try again -> schedule -> again ...
 -> hit -> __mutex_trylock_or_owner() -> locked!
```

## Memory Allocation

```
kmalloc()
linux/slab.h:kmalloc
 -> large (size > KMALLOC_MAX_CACHE_SIZE)
    -> kmalloc_large()
 -> small -> __do_kmalloc or __do_kmalloc_node
```
