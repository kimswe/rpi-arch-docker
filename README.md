rpi-arch-docker
===============
Updated version of docker installscript, and some stuff to get it all running.

After Arch Install, resize partition
---

```sh
fdisk "/dev/mmcblk0"
p 
d # delete
2 
n #new
e 
(return) # accept default partition no
(return) # accept default start
(return) # accept default end
n
l
(return) # accept default start
(return) # accept default end
p
w

sync; reboot 
...
resize2fs /dev/mmcblk0p5
```

Download and install
---
```sh
curl https://raw.github.com/kimswe/rpi-arch-docker/master/install.sh | sh
```
