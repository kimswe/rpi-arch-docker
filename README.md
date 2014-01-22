rpi-arch-docker
===============
Updated version of docker installscript, and some stuff to get it all running.

Original at https://github.com/resin-io/docker-install-script

Something is weird, the installscript works sometimes and sometimes not. Seems pacman is Killed by the kernel or something. Perhaps resizing the partitions screwed with the swap drives or something.

Reflashed, downloaded packages manually, and ran the install via pacman.

After Docker Install, resize partition
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


Startup
-----
WHy is my docker.service file not installed? Well it is, i just have to start the service using `systemctl start docker.service`




Ghost
----
https://github.com/resin-io/docker-nginx-ghost

Google Coder
----
docker run -d -p 8081:8081 resin/rpi-google-coder



Download and install
---
```sh
curl https://raw.github.com/kimswe/rpi-arch-docker/master/install.sh | sh
```


