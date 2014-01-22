# rpi-arch-docker

Updated version of docker installscript, and some stuff to get it all running.

Original at https://github.com/resin-io/docker-install-script

Something is weird, the installscript works sometimes and sometimes not. Seems pacman is 'Killed' by the kernel. Could be slow internet, low ram or something. 

I did a reflash, manually downloaded the packages and ran `pacman -U packagename.tar.xz` for all packages, and finally, success!

##Download and install
    curl https://raw.github.com/kimswe/rpi-arch-docker/master/install.sh | sh
Might work for you, who knows.

## After Docker Install, resize partition


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


## Run docker on startup

Why is my docker.service file not installed in /etc/system? Well it is, i just have to start the service using `systemctl start docker.service`


##Services
###Ghost
https://github.com/resin-io/docker-nginx-ghost

###Google Coder
    docker run -d -p 8081:8081 resin/rpi-google-coder




 
 
##Pacman cheat sheet
```
pacman -Sy       # synchronize repository databases if neccessary
pacman -Syy      # force synchronization of repository databases

pacman -Ss xyz   # search repository database for packages for xyz
 
pacman -S xyz    # install package xyz
pacman -Sy xyz   # synchronize repo and install xyz
pacman -Syy xyz  # really synchronize repo and install xyz
 
pacman -R xyz    # remove package xyz but keep its dependencies installed
pacman -Rs xyz   # remove package xyz and all its dependencies (if they are not required by any other package)
pacman -Rsc xyz  # remove package xyz, all its dependencies and packages that depend on the target package
 
pacman -Ql xyz   # show all files installed by the package xyz
pacman -Qo /path # find the package which installed the file at /path**strong text**

```