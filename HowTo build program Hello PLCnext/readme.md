# How to build a simple "Hello PLCnext" application

> Based on the official [documentation](https://github.com/PLCnext/SampleRuntime/blob/master/getting-started/Part-01/README.md).

## Using command line (pure **CMake**)

After cloning repository execute this steps inside `"HowTo build program Hello PLCnext\Hello-PLCnext"` working direcrory.

Configure:

```sh
cmake --preset=build-windows-AXCF2152-2021.0.3.35554 .
```

Build:

```sh
cmake --build --preset=build-windows-AXCF2152-2021.0.3.35554 --target all
```

Deploy:

```sh
cmake --build --preset=build-windows-AXCF2152-2021.0.3.35554 --target install
```

In above commands the `build-windows-AXCF2152-2021.0.3.35554` preset name specifies build parameters on OS Windows for AXC 2152. It is stored in `"HowTo build program Hello PLCnext\Hello-PLCnext\CMakePresets.json"` file. Inside this file you can found parameters:

- The `PLCNEXT_SDK_ROOT` parameter specifies the full path to the root directory of the SDK.
- The `ARP_DEVICE` and `ARP_DEVICE_VERSION` parameters should specify the SDK device and version.

You can change it, if necessary, to the SDK device, version and path of the SDK that you are using.

After you can find executable here:

> deploy\AXCF2152_21.0.3.35554\Release\bin\hello_PLCnext

On **Linux OS** use `build-linux-AXCF2152-2021.0.3.35554` preset name.

## Using MS Visual Code

Open directory `"HowTo build program Hello PLCnext\Hello-PLCnext"` in MS Visual Code.
To work correctly, you need to install the CMake, CMake Tools extension. You also need to specify the path to ninja.exe to build the project. Open the CMakeCache file, which has the path How To build programm `"Hello PLCnext\Hello-PLCnext\bin\AXCF2152_2020.6.1"` In this file, look for the line `"CMAKE_MAKE_PROGRAM:FILEPATH="`and write here the path to ninja.exe `"C:\Program Files (x86)\Microsoft Visual Studio\2019\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\Ninja\ninja.exe"` Save the project, restart, and build the project.

## Using MS Visual Studio 2019 Community (Windows OS)

Open directory `"HowTo build program Hello PLCnext\Hello-PLCnext"` in MS Visual Studio.

Thus you have opened CMake-based project. Set auto-suggested configuration and build the application (press **F7** to start build process).

## Using other IDE which support CMake presets

Open directory `"HowTo build program Hello PLCnext\Hello-PLCnext"` in IDE.

Thus you have opened CMake-based project. Set auto-suggested configuration and build the application.
