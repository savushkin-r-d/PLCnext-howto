# How to build a simple "Hello PLCnext" application #

> Based on the official [documentation](https://github.com/PLCnext/SampleRuntime/blob/master/getting-started/Part-01/README.md).

## 1. Using command line (pure **CMake**) ##

Configure:
```sh
cmake -E env PLCNEXT_SDK_ROOT="c:\CLI\SDKs\AXCF2152\2021_0" ARP_DEVICE="AXCF2152" ARP_DEVICE_VERSION="2021.0.3 LTS (21.0.3.35554)" cmake --preset=default .
```

Build:
```sh
cmake -E env PLCNEXT_SDK_ROOT="c:\CLI\SDKs\AXCF2152\2021_0" ARP_DEVICE="AXCF2152" ARP_DEVICE_VERSION="2021.0.3 LTS (21.0.3.35554)" cmake --build --preset=default
```

Deploy:
```sh
cmake -E env PLCNEXT_SDK_ROOT="c:\CLI\SDKs\AXCF2152\2021_0" ARP_DEVICE="AXCF2152" ARP_DEVICE_VERSION="2021.0.3 LTS (21.0.3.35554)" cmake --build --preset=default --target install
```

In above commands:
 - The PLCNEXT_SDK_ROOT parameter specifies the full path to the root directory of the SDK. Please change this, if necessary, to the path of the SDK that you are using.
 - The ARP_DEVICE and ARP_DEVICE_VERSION parameters should specify the SDK device and version. Please change these if necessary.

After you can find executable here:
>deploy\AXCF2152_21.0.3.35554\Release\bin\hello_PLCnext

## 2. Using Windows OS and MS Visual Studio 2019 Community ##

Set required environment variable **PLCNEXT_SDK_ROOT** - it specifies the full path to the root directory of the SDK. Please change this, if necessary, to the path of the SDK that you are using:

```sh
setx PLCNEXT_SDK_ROOT "c:\CLI\SDKs\AXCF2152\2021_0"
```

Open directory **Hello-PLCnext** in MS Visual Studio. Example using command line:

```sh
"%ProgramFiles(x86)%\Microsoft Visual Studio\2019\Community\Common7\IDE\devenv.exe" ./Hello-PLCnext
```

Thus you have opened CMake-based project. Build the application (press **F7** to start build process).

## 3. Using JetBrains IDE CLion 2021.2.3 ##

Set required environment variable **PLCNEXT_SDK_ROOT** - it specifies the full path to the root directory of the SDK. Please change this, if necessary, to the path of the SDK that you are using. On Windows use this command:

```sh
setx PLCNEXT_SDK_ROOT "c:\CLI\SDKs\AXCF2152\2021_0"
```

On Linux use this command:

```sh
export PLCNEXT_SDK_ROOT="/opt/pxc/SDKs/AXCF2152/2021_0"
```

Open directory **Hello-PLCnext** in CLion. Thus you have opened CMake-based project. Build the application (press **F7** to start build process).
