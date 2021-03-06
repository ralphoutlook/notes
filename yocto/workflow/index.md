### Developing a Board Support Package (BSP)
---
  - Set up your host development system to support development using the Yocto Project
  - Establish a local copy of the project files on your system
  - Establish the meta-intel repository on your system
  - Create your own BSP layer using the yocto-bsp script
  - Make configuration changes to your new BSP layer
  - Make recipe changes to your new BSP layer
  - Prepare for the build
  - Build the image

### Set up your host development system to support development using the Yocto Project
---
  Ubuntu and Debian
  - Essentials: Packages needed to build an image on a headless system:
    ```
    $ sudo apt-get install gawk wget git-core \
        diffstat unzip texinfo gcc-multilib \
        build-essential chrpath socat
    ```
  - Graphical and Eclipse Plug-In Extras: Packages recommended if the host system has graphics support or if you are going to use the Eclipse IDE:
    ```
    $ sudo apt-get install libsdl1.2-dev xterm
    ```
  - Documentation: Packages needed if you are going to build out the Yocto Project documentation manuals:
    ```
    $ sudo apt-get install make xsltproc docbook-utils fop dblatex xmlto
    ```
  - SDK Installer Extras: Packages needed if you are going to be using the the standard or extensible SDK:
    ```
    $ sudo apt-get install autoconf automake libtool libglib2.0-dev libarchive-dev
    ```
  - OpenEmbedded Self-Test (oe-selftest): Packages needed if you are going to run oe-selftest:
    ```
    $ sudo apt-get install python-git
    ```

