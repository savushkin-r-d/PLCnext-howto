# How to use **valgrind** #

## 1. Building **valgrind** (on Linux) ##

> Based on the official [documentation](https://valgrind.org/downloads/repository.html).

Clone **valgrind** source code repository:

```sh
git clone git://sourceware.org/git/valgrind.git
```

Cloning should finish successfully:
```sh
Cloning into 'valgrind'...
remote: Enumerating objects: 132463, done.
remote: Counting objects: 100% (132463/132463), done.
remote: Compressing objects: 100% (31192/31192), done.
remote: Total 132463 (delta 101212), reused 126261 (delta 96216), pack-reused 0
Receiving objects: 100% (132463/132463), 44.84 MiB | 6.33 MiB/s, done.
Resolving deltas: 100% (101212/101212), done.
Updating files: 100% (6435/6435), done.
```

Change current directory:
```sh
cd valgrind
```

Run autoconf:
```sh
./autogen.sh
```

Autoconf should finish successfully:
```sh
running: aclocal
running: autoheader
running: automake -a
configure.ac:53: installing './compile'
configure.ac:224: installing './config.guess'
configure.ac:224: installing './config.sub'
configure.ac:37: installing './install-sh'
configure.ac:37: installing './missing'
Makefile.vex.am: installing './depcomp'
running: autoconf
```

Setup environment (to be able to crosscompile):
```sh
source /opt/pxc/sdk/AXCF2152/2020.0/environment-setup-cortexa9t2hf-neon-pxc-linux-gnueabi
```

where `/opt/pxc/sdk/AXCF2152/2020.0` - your sdk path.

Configure:
```sh
./configure --host=armv7-linux-gnueabi --prefix=/opt/valgrind
```

Build:
```sh
make
```

Add link to ranlib:
```sh
sudo ln -s /usr/bin/ranlib /usr/bin/arm-pxc-linux-gnueabi-ranlib
```

Install:
```sh
sudo make install
```
## 2. Deploying **valgrind** to a controller ##

Copy directory `/opt/valgrind` to controller to the directory `/opt/valgrind` (using **WinSCP**).

Make executable:
```sh
su
cd /opt/valgrind/bin
chmod +x ./*
cd /opt/valgrind/libexec/valgrind
chmod +x ./memcheck-arm-linux
```

Make symbolic link:
```sh
ln -s /opt/valgrind/libexec /usr/local/libexec
```

Check valgrind:
```sh
/opt/valgrind/bin/valgrind --version
```

Correct output should be:
```sh
valgrind-3.19.0.GIT
```

Check with extra information:
```sh
/opt/valgrind/bin/valgrind -d -v
```

Correct output should be:
```sh
--1667:1:debuglog DebugLog system started by Stage 1, level 1 logging requested
--1667:1:launcher no tool requested, defaulting to 'memcheck'
--1667:1:launcher no client specified, defaulting platform to 'arm-linux'
--1667:1:launcher launching /usr/local/libexec/valgrind/memcheck-arm-linux
--1667:1:debuglog DebugLog system started by Stage 2 (main), level 1 logging requested
--1667:1:    main Welcome to Valgrind version 3.19.0.GIT debug logging
--1667:1:    main Checking current stack is plausible
--1667:1:    main Checking initial stack was noted
--1667:1:    main Starting the address space manager
--1667:1:    main Address space manager is running
--1667:1:    main Starting the dynamic memory manager
--1667:1:mallocfr newSuperblock at 0x615AA000 (pszB 4194288)  owner VALGRIND/core
--1667:1:mallocfr deferred_reclaimSuperblock at 0x615AA000 (pszB 4194288)  (prev 0x0) owner VALGRIND/core
--1667:1:    main Dynamic memory manager is running
--1667:1:    main Initialise m_debuginfo
--1667:1:    main VG_(libdir) = /usr/local/libexec/valgrind
--1667:1:    main Getting launcher's name ...
--1667:1:    main ... /opt/valgrind/bin/valgrind
--1667:1:    main Get hardware capabilities ...
--1667:1: machine ARMv7 VFP 1 VFP2 1 VFP3 1 NEON 1
--1667:1:   cache Could not autodetect cache info
--1667:1:    main ... arch = ARM, hwcaps = ARMv7-neon-vfp
--1667:1:    main Getting the working directory at startup
--1667:1:    main ... /opt/valgrind/bin
--1667:1:    main Split up command line
--1667:1:    main (early_) Process Valgrind's command line options
--1667:1:    main Create initial image
--1667:1: initimg Loading client
valgrind: no program specified
valgrind: Use --help for more information.
```

## 3. Deploying libraries with debug information to a controller ##

Copy files from `\opt\pxc\sdk\AXCF2152\2020.0\sysroots\cortexa9t2hf-neon-pxc-linux-gnueabi\lib\.debug\` (PC) to `\lib\.debug\` (controller).

