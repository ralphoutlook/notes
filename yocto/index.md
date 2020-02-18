### index
- [devtool](#devtool)
- [bitbake](#bitbake)
- [poky](#poky)

### reference
- [yocto project wiki](https://wiki.yoctoproject.org/wiki/Main_Page)
- [quick start](https://www.yoctoproject.org/docs/2.4.2/yocto-project-qs/yocto-project-qs.html)
- [reference guide](https://www.yoctoproject.org/docs/current/ref-manual/ref-manual.html)
- [application developer's guide](https://www.yoctoproject.org/docs/1.8.2/adt-manual/adt-manual.html)
- [bitbake guide](https://bitbucket.org/a4z/bitbakeguide/src/master/)
- [bitbake useful commands](#bitbake)


### ubuntu essential needed packages
```
$ sudo apt-get install -y gawk wget git-core diffstat unzip \
    texinfo gcc-multilib build-essential chrpath socat cpio \
    python python3 python3-pip python3-pexpect xz-utils debianutils \
    iputils-ping libsdl1.2-dev xterm
```  

for doc 
```
# only for devtool add giflib
$ sudo apt-get install -y xmlto
$ sudo apt-get install make xsltproc docbook-utils fop dblatex xmlto
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

### build core-minimal-image
-vDDD: show build log 
```
$ bitbake core-image-minimal -vDDD
```
more information...
```
Build Configuration:
BB_VERSION           = "1.44.0"
BUILD_SYS            = "x86_64-linux"
NATIVELSBSTRING      = "universal"
TARGET_SYS           = "x86_64-poky-linux"
MACHINE              = "qemux86-64"
DISTRO               = "poky"
DISTRO_VERSION       = "3.0+snapshot-20200218"
TUNE_FEATURES        = "m64 core2"
TARGET_FPU           = ""
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

build giflib
```
$ devtool build giflib
```

giflib built objects
```
$ find tmp/work/*-poky-linux -mindepth 1 -maxdepth 1 -type d -name "giflib*"
```

### recipetool
create recipe files folder
```
$ mkdir -p meta-layer/recipes-myproject/myproject/files
```

in `meta-layer/recipes-myproject/myproject/files`:    
hello.c
```
SRCS := $(wildcard *.c)
OBJS := $(SRCS:.c=.o)
# hello
HELLO_OBJS := $(filter hello%.o, $(OBJS))
TARGET_HELLO := hello
# targets
TARGET :=  $(TARGET_HELLO)
# varables used in yocto
bindir ?= /usr/bin

LIBS :=

.PHONY: clean all

all: $(TARGET)

%.o : %.c
 $(CC) -c $< -o $@ ${LDFLAGS} ${LIBS}

$(TARGET_HELLO) : $(OBJS)
 $(CC) $(HELLO_OBJS) -o $@ ${LIBS} ${LDFLAGS}

install:
 install -d $(DESTDIR)$(bindir)
 install -m 755 $(TARGET_HELLO) $(DESTDIR)$(bindir)/
```
hello.h
```
#ifndef HELLO_EXAMPLE_H
#define HELLO_EXAMPLE_H
/*
 * Example function
 */
extern void LibHelloWorld(void);

#endif /* HELLO_EXAMPLE_H */
```
hellolib.c
```
#include <stdio.h>
#include "hello.h"

void LibHelloWorld()
{
  printf("Hello World (from a shared library!)\n");
}
```
Makefile
```
SRCS := $(wildcard *.c)
OBJS := $(SRCS:.c=.o)
# hello
HELLO_OBJS := $(filter hello%.o, $(OBJS))
TARGET_HELLO := hello
# targets
TARGET :=  $(TARGET_HELLO)
# varables used in yocto
bindir ?= /usr/bin

LIBS :=

.PHONY: clean all

all: $(TARGET)

%.o : %.c
        $(CC) -c $< -o $@ ${LDFLAGS} ${LIBS}

$(TARGET_HELLO) : $(OBJS)
        $(CC) $(HELLO_OBJS) -o $@ ${LIBS} ${LDFLAGS}

install:
        install -d $(DESTDIR)$(bindir)
        install -m 755 $(TARGET_HELLO) $(DESTDIR)$(bindir)/
```

### bitbake
basic bitbake tree
```
├── bb.mk
├── bb.sh
├── conf
│   └── bblayers.conf
├── macro.mk
├── Makefile
├── meta-first
│   ├── classes
│   │   ├── base.bbclass
│   │   └── base.bbclass.test
│   ├── conf
│   │   ├── bitbake.conf
│   │   └── layer.conf
│   └── recipes-first
│       └── first
│           └── first_0.1.bb
└── rules.mk
```

what is layer?
```
# meta*
$ find -type d -mindepth 1-maxdepth 1 -name "meta*" 
```

what is recipe?
```
$ find -name "*.bb"
```

How to use *.bbclass?
```
# *.bb
  inherit xxx
    -> include xxx.bbclass
  *.bbclass in  meta-*/classes (layers classes)
# command to find inherit
  $ find -name *.bb | grep ^inherit
```

install bitbake by git fetch
```
$ (version=1.32; git clone -b ${version} https://github.com/openembedded/bitbake.git)
```

Bake an image (add -k to continue building 
even errors are found in the tasks execution)
```
$ bitbake <image>
```

Execute a particular package's task. Default 
Tasks names: fetch, unpack, patch, configure, 
compile, install, package, package_write, and 
build.
```
$ bitbake <package> -c <task>	
```

Example: To (force) compiling a kernel and 
then build, type:
```
$ bitbake linux-imx -f -c compile
$ bitbake linux-imx
```

Show the package dependency for image.
```
$ bitbake <image > -g -u depexp
```

Example: To show all packages included on fsl-image-gui
```
$ bitbake fsl-image-gui -g -u depexp
```
NOTE: This command will open a UI window, so it must be execute on a 
console inside the host machine (either virtual or native).

Open a new shell where with neccesary system values already defined for package hob bitbake frontend/GUI.
```
$ bitbake <package> -c devshell
```

List all tasks for package
```
$ bitbake <package> -c listtasks
```

Interactive kernel configuration
```
$ bitbake virtual/kernel -c menuconfig
```

Fetch sources for a particular image
```
$ bitbake <image> -c fetchall
```

Show layers
```
$ bitbake-layers show-layers	
```

Show possible images to bake. Without "*-images-*", it shows ALL recipes
```
$ bitbake-layers show-recipes "*-image-*"	
```

Show image's packages
```
$ bitbake -g <image> && cat pn-depends.dot | grep -v -e '-native' | grep -v digraph | grep -v -e '-image' | awk '{print $1}' | sort | uniq
```

Show package's dependencies
```
$ bitbake -g <pkg> && cat pn-depends.dot | grep -v -e '-native' | grep -v digraph | grep -v -e '-image' | awk '{print $1}' | sort | uniq
```

Print (on console) and store verbose baking
```
$ bitbake –v <image> 2>&1 | tee image_build.log
```

Check if certain package is present on current Yocto Setup
```
$ bitbake -s | grep <pkg>
```

force to do package's task again
```
$ bitbake <package> -C <task> 
$ bitbake <package> -c <task>  -f
```

check kernel version
```
# nxp i.mx6
$ bitbake -e linux-imx | grep "^PV"
# x86
$ bitbake -e virtual/kernel | grep "^PV"
```

### poky
check poky version
```
# nxp i.mx6
$ grep "^DISTRO_VERSION *=" $BSPDIR/sources/poky/meta-poky/conf/distro/poky.conf
```






