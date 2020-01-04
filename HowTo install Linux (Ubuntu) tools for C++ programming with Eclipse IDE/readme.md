# How to configure Eclipse® to program and crosscompile for the AXC F 2152 on Ubuntu 18.04 LTS #

> This HowTo only works for the AXC F 2152 firmware version 2019.3. For other devices or FW versions the build flags are different and could change from version to version.

## 1. Install **Eclipse®** IDE ##

1. Check whether **JRE** is already installed or not. The latest **Java SE** is recommended:

```sh
java -version
```
![java version](images/java_-version.png)

If not installed, install **OpenJdk**:

```sh
sudo apt-get install openjdk-11-jre
```

Afterwards, the check should look like this:

![java version ok](images/java_-version_ok.png)

2. To install **Eclipse IDE for C/C++ Developers** visit https://www.eclipse.org/downloads/packages/, select and download appropriate package:

![eclipse package](images/eclipse_package.png)

or use wget to download **2019.3 R** version (risk of being changed):

```sh
wget -P ~/Downloads http://ftp.snt.utwente.nl/pub/software/eclipse//technology/epp/downloads/release/2019-03/R/eclipse-cpp-2019-03-R-linux-gtk-x86_64.tar.gz
```

Extract the „eclipse-cpp-2019-03-R-linux-gtk-x86_64.tar.gz“:

```sh
cd ~/Downloads
tar -xzf eclipse-cpp-2019-03-R-linux-gtk-x86_64.tar.gz
```

> **Hint:** Move the extracted folder to */opt*. The **Opt**ional folder is typically for programs not installed via a packagemanager and in contrast to the home folder, it is accessable for any user on the system.
>
> \> sudo mv eclipse /opt/

Create a desktop launcher for Eclipse:

```sh
sudo nano /usr/share/applications/eclipse.desktop
```
Copy the following into the desktop file:

```sh
[Desktop Entry]
Name=Eclipse
Type=Application
Exec=/opt/eclipse/eclipse
Terminal=false
Icon=/opt/eclipse/icon.xpm
Comment=Integrated Development Environment
NoDisplay=false
Categories=Development;IDE
Name[en]=eclipse.desktop
```

Create a symlink to make eclipse avaible from the console:

```sh
cd /usr/local/bin
sudo ln -s /opt/eclipse/eclipse
```

**Eclipse** is now ready to use.

## 3. Install the Toolchain ##

Unzip **SDK**:

Download the needed SDK from the Phoenix Contact webside.

[LINK](http://www.phoenixcontact.com/qr/2404267/softw)

Navigate to the folder where your SDK is located.

```sh
unzip SDK_Linux64_2019.3.zip
```

Install **SDK**:

```sh
chmod +x ./pxc-glibc-x86_64-axcf2152-image-sdk-cortexa9t2hf-neon-toolchain-2019.3.sh
./pxc-glibc-x86_64-axcf2152-image-sdk-cortexa9t2hf-neon-toolchain-2019.3.sh
```

## 4. Configure Eclipse® IDE to use the installed PLCnext SDK ##

Set project cross settings (prefix and path):

>arm-pxc-linux-gnueabi-  
>/opt/pxc/sdk/AXCF2152/2019.3/sysroots/x86_64-pokysdk-linux/usr/bin/arm-pxc-linux-gnueabi

![SDK ok](images/cdt_cross_settings.png)

Set project cross G++ Compiler dialect settings:

>-march=armv7-a -mthumb -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a9 --sysroot=/opt/pxc/sdk/AXCF2152/2019.3/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi -fno-gnu-unique

![SDK ok](images/cdt_dialect_flags.png)

Set project cross G++ Preprocessor defines:

>ARP_DEVICE_AXCF2152

![SDK ok](images/cdt_defines.png)

Set project cross G++ Preprocessor includes:

>/opt/pxc/sdk/AXCF2152/2019.3/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi/usr/include/plcnext

![SDK ok](images/cdt_includes.png)

Set project cross G++ Linker flags:

>--sysroot=/opt/pxc/sdk/AXCF2152/2019.3/sysroots/cortexa9t2hf-neon-pxc-linux-gnueabi -march=armv7-a -mthumb -mfpu=neon -mfloat-abi=hard -mcpu=cortex-a9 -Wl,--no-undefined

![SDK ok](images/cdt_cross_linker_settings.png)
