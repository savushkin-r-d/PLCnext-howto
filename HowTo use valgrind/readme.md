# How to use **valgrind** #

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

Copy directory `/opt/valgrind` to controller to the directory `/opt/valgrind` using **WinSCP**.

Make executable:

```sh
cd /opt/valgrind/bin
sudo chmod +x ./valgrind ./callgrind_annotate ./callgrind_control ./cg_annotate ./cg_diff ./cg_merge ./ms_print ./valgrind-di-server ./valgrind-listener ./vgdb
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

Download package `libc6-dbg` from this link: 
https://packages.debian.org/sid/armhf/libc6-dbg/download.
https://packages.debian.org/buster/armhf/libc6-dbg/download

Copy it to the controller to `/opt/valgrind/`. Then install:

```sh
sudo dpkg --install /opt/valgrind/libc6-dbg_2.33-5_armhf.deb
```

