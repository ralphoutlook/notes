
### reference
- [yocto project wiki](https://wiki.yoctoproject.org/wiki/Main_Page)
- [quick start](https://www.yoctoproject.org/docs/2.4.2/yocto-project-qs/yocto-project-qs.html)
- [reference guide](https://www.yoctoproject.org/docs/current/ref-manual/ref-manual.html)
- [application developer's guide](https://www.yoctoproject.org/docs/1.8.2/adt-manual/adt-manual.html)

### ubuntu essential needed packages
```
$ sudo apt-get install -y gawk wget git-core diffstat unzip \
    texinfo gcc-multilib build-essential chrpath socat cpio \
    python python3 python3-pip python3-pexpect xz-utils debianutils \
    iputils-ping libsdl1.2-dev xterm
```  

### list all tags and branches fpr poky git repository 
```
$ git ls-remote git://git.yoctoproject.org/poky
```

### clone poky 
```
$ git clone --depth=1 -b $pokyver git://git.yoctoproject.org/poky $pokydir
```
or
```
$ git clone git://git.yoctoproject.org/poky
$ cd poky
$ git checkout tags/yocto-2.4.2 -b poky_2.4.2
```

### set up the poky environment 
```
$ cd $pokydir $ . oe-init-build-env
```

### build the core-minimal-image
-vDDD: show build log 
```
$ bitbake core-image-minimal -vDDD
```

### create layer 
```
$ bitbake-layers create-layer meta-layer
```

### add layer 
```
$ bitbake-layers add-layer meta-layer
```

### list files after create layer 
```
$ ls
bitbake-cookerdaemon.log cache conf downloads meta-layer sstate-cache tmp
```

### devtool 
add git open source, ex: giflib
```
$ devtool add giflib git://git.code.sf.net/p/giflib/code
```
then, list workspace
```
$ ls . workspace/recipes/giflib/
.:
bitbake-cookerdaemon.log  downloads               sstate-cache
cache                     log.core-image-minimal  tmp
conf                      meta-layer              workspace

workspace/recipes/giflib/:
giflib_git.bb
```


