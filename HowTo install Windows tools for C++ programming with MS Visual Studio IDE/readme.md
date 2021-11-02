# How to configure MS Visual Studio Community® to program and crosscompile for the AXC F **x**152 controllers on Windows 10 #

> This HowTo only works for AXC F **x**152 controllers and the AXC F firmware version 2021.9. For other devices or FW versions the instructions could change from version to version.

> Based on the official [documentation](https://www.plcnext.help/te/Programming/Cpp/Cpp-programming.htm).

## 1. Installing **MS Visual Studio Community®** IDE ##

1. To install **Visual Studio Community®** visit https://visualstudio.microsoft.com/, select and download Community version.

## 2. Installing (updating) the PLCnext CLI ##

>The **PLCnext CLI** is a command line interface that can be used for generating metadata, C++ header files, PLCnext Engineer libraries and for the build process. The functions can be called using simple commands. An integrated help lists the commands and describes their functions.

Download the latest version from the Phoenix Contact website https://www.phoenixcontact.com/products (for example from the **AXC F 2152** area - http://www.phoenixcontact.com/qr/2404267/softw, current is `2021.6`).

Navigate to the folder where downloads are located (typical path `%userprofile%/Downloads`), unzip the archive (`PLCnext_Toolchain_WindowsSetup_.zip`).

Navigate to the folder where downloads are previously unzipped, run the installation file (`PLCnext_Toolchain_WindowsSetup.exe`) and follow instructions of the installation wizard.

![SDK ok](images/PLCNCLI_setup.png)

>To update just start the installer and make sure to install to the same directory the previous PLCnext CLI was installed in.

Check installation:

```ps
plcncli.exe --version
```

Afterwards, the check should look like this:

```ps
plcncli 21.6.0.726 (21.6.0.726)
```
## 3. Downloading PLCnext Technology C++ Toolchain ##

Download the latest version from the Phoenix Contact website https://www.phoenixcontact.com/products (for example from the **AXC F 2152** area - http://www.phoenixcontact.com/qr/2404267/softw, current is `2021.9`).

Navigate to the folder where downloads are located (typical path `%userprofile%/Downloads`), unzip the archive (`SDK_2021.9_Windows_AXC_F_2152.tar.xz.zip`).

## 3. Installing (updating) the SDK ##

Navigate to the folder where downloads are previously unzipped, Call the CLI in the console using the following command:

```ps
plcncli.exe install sdk –d [installation path] –p [path to archive file]
```

>If you install several SDKs, Phoenix Contact recommends to use the "target name/firmware version" folder structure.

E.g.:

```ps
plcncli.exe install sdk -d C:\CLI\SDKs\AXCF2152\2021_9\ -p pxc-glibc-x86_64-mingw32-axcf2152-image-mingw-cortexa9t2hf-neon-axcf2152-toolchain-2021.9.tar.xz
```

>The SDK is specified to the controller. The full list of controllers can be found on the PHOENIX CONTACT International site ([Home > Products > PLCs and I/O systems > PLCnext Control > Product list PLCnext Technology components](https://www.phoenixcontact.com/online/portal/pi?1dmy&urile=wcm%3apath%3a/pien/web/main/products/list_pages/PLCnext_technology_components_P-21-14-01/f77f0eb0-2a70-40c3-8679-7df2450e26db)).

## 4. Creating a new C++ project in Visual Studio ##

Now you can create a C++ project from a **PLCnext** template. Start Visual Studio, select `"Create a new project"` and search for **plcnext** in the Dialog box to show the **PLCnext** project templates and select the template that fits your needs, then click Next.

More information is located [here](https://www.plcnext.help/te/Programming/Cpp/Cpp_programming/Creating_a_Cpp_project_in_Visual_Studio.htm).

## 5. Opening existed C++ project in Visual Studio ##

Due to a known [issue](https://github.com/PLCnext/PLCnext_CLI_VS/issues/4) you might get compile-time errors, to fix this you have to delete the local .NET cache:

```ps
rmdir %temp%\.net /s
```
