# Transparent Caching Server Control Plane V1.4 #

These notes provide instructions on howto download and install the Laguna Transparent Caching Server Control Plane on 64-bit Linux CentOS-7 systems. Ensure at least the *Compatibility libraries* and *Development Tools* group of packages are available on the build server, in addition others may be required--use *yum* to resolve these package dependencies.

See *centos7-scripts/SCRIPTS* directory for scripts to help setup build and deployment systems.

**Step-by-step guide**

Firstly, create a working sandbox into which download and build the libraries and/or packages specified in steps 1-8 before attempting to build the TCS Control Plane application outlined in step 9 below.
 
**1) [C YAML File Parser Library](http://pyyaml.org/wiki/LibYAML)**

    Download http://pyyaml.org/download/libyaml/yaml-0.1.5.tar.gz
    tar -zxvf yaml-0.1.5.tar.gz
    ./configure
    make
    sudo make install && ldconfig
  
**2) [C Logging Library](https://github.com/HardySimpson/zlog)**

    Download zlog https://github.com/HardySimpson/zlog/archive/latest-stable.tar.gz
    tar -zxvf zlog-latest-stable.tar.gz
    cd zlog-latest-stable/
    make
    sudo make install && ldconfig
  
**3) [C JSON library](http://www.digip.org/jansson)**

    Download jansson http://www.digip.org/jansson/releases/jansson-2.7.tar.gz
    tar –zxvf jansson-2.7.tar.gz
    ./configure
    make
    make check
    sudo make install && ldconfig
  
**4) [ZeroMQ Distrubuted Messaging Library](http://zeromq.org)**

    Dowload zeromq http://download.zeromq.org/zeromq-4.1.3.tar.gz
    Make sure that libsodium, libtool, pkg-config, build-essential, autoconf, and automake are installed.
    Check whether uuid-dev package, uuid/e2fsprogs RPM or equivalent on your system is installed
    ./configure
    make
    make check
    sudo make install && ldconfig
  
**5) [C Binding for ZeroMQ Library](https://github.com/zeromq/czmq/releases)**

    Download czmq https://github.com/zeromq/czmq/archive/v3.0.2.tar.gz
    ./autogen.sh
    ./configure 
    make
    make check 
    sudo make install && ldconfig
  
**6) [PF_RING™ Linux kernel module and user-space packet processing framework](https://github.com/ntop)**

    git clone https://github.com/ntop/PF_RING.git
    cd PF_RING/kernel
    make
    sudo make install
    cd ../userland/lib
    sudo make install
    sudo insmod ./pf_ring.ko
 
**7) [C Lock-free Data Structure Library](http://www.liblfds.org)**

    git clone https://github.com/liblfds/liblfds6.1.1
    cd liblfds6.1.1/liblfds611
    mkdir bin; mkdir obj
    make –f makefile.linux ardbg
    sudo cp inc/liblfds611.h usr/local/include
    sudo cp bin/liblfds611.a /usr/local/lib
  
**8) [C Prototyping Tools Library provides cp_mempool](http://cprops.sourceforge.net)**

    Download http://sourceforge.net/projects/cprops/files/cprops/cprops-0.1.12/libcprops-0.1.12.tar.gz
    tar –zxvf libcprops-0.1.12.tar.gz
    cd libcprops-0.1.12
    ./configure
    make
    sudo make install && ldconfig

**9) [C Transparent Caching Server Control Plane](https://github.com/concurrentlabs/laguna)**

    git clone https://github.com/concurrentlabs/laguna
    Ensure soft link /usr/lib64/libpcap.so -> libpcap.so.1.5.3 exists
    cd 1.0
    make release
    make package
  
**10) [Install TCS Package]()**

    rpm -ivh install/rpm/x86_64/release/RPMS/x86_64/transparent_caching-1.4.1-1.x86_64.rpm
