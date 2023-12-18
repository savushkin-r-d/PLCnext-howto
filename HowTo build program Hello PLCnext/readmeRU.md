# Как создать простое приложение "Hello PLCnext" #

> [!IMPORTANT]
> Основано на официальной [документации](https://github.com/PLCnext/SampleRuntime/blob/master/getting-started/Part-01/README.md).

> [!TIP]
> English version is [here](./readmeEN.md).

## Использование командной строки (чистый **CMake**) ##

После клонирования репозитория выполните следующие действия в рабочей директории  `"HowTo build program Hello PLCnext\Hello-PLCnext"`.

Конфигурирование:
```sh
cmake --preset=build-windows-AXCF2152-2021.0.3.35554 .
```

Сборка:
```sh
cmake --build --preset=build-windows-AXCF2152-2021.0.3.35554 --target all
```

Развертывание:
```sh
cmake --build --preset=build-windows-AXCF2152-2021.0.3.35554 --target install
```

В приведенных выше командах имя предустановки `build-windows-AXCF2152-2021.0.3.35554` определяет параметры сборки в ОС Windows для AXC 2152. Оно хранится в файле `"HowTo build program Hello PLCnext\Hello-PLCnext\CMakePresets.json"`. Внутри этого файла вы можете найти параметры:

 - Параметр `PLCNEXT_SDK_ROOT` указывает полный путь к корневому каталогу SDK.
 - Параметры`ARP_DEVICE` и `ARP_DEVICE_VERSION` должны указывать устройство и версию SDK.

При необходимости вы можете изменить их на используемые.

После развертывания вы сможете найти исполняемый файл здесь:

>deploy\AXCF2152_21.0.3.35554\Release\bin\hello_PLCnext

В **ОС Linux** используйте предустановленное имя `build-linux-AXCF2152-2021.0.3.35554`.

## Использование MS Visual Code ##

Откройте каталог `"HowTo build program Hello PLCnext\Hello-PLCnext"` в MS Visual Code.

Таким образом, вы открыли проект на основе CMake. Установите автоматически предлагаемую конфигурацию и создайте приложение.

## Использование MS Visual Studio 2019 Community (ОС Windows) ##

Откройте каталог `"HowTo build program Hello PLCnext\Hello-PLCnext"` в MS Visual Studio.

Таким образом, вы открыли проект на основе CMake. Установите автоматически предлагаемую конфигурацию и создайте приложение (нажмите **F7** , чтобы начать процесс сборки).

## Использование другой IDE, которая поддерживает предустановки CMake##

Откройте каталог `"HowTo build program Hello PLCnext\Hello-PLCnext"` в IDE.

Таким образом, вы открыли проект на основе CMake. Установите автоматически предлагаемую конфигурацию и создайте приложение.
