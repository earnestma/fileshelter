# FileShelter
FileShelter is a self-hosted software that allows you to easily share files over the Internet.
Just upload a file and get an URL back!

The aim is to provide a very simple web application, with few package dependencies, so that anyone can install it on his own server.

A [demo](http://fileshelter.suroot.com) instance is available, with the following limitations:
- Maximum duration is set to 3 days
- Maximum download limit is set to 10
- Maximum file size is set to 1 MB

## Features
- Period of validity (from one hour to years)
- Optional download limit
- Optional password protection
- Practically unique links, using [UUID](https://fr.wikipedia.org/wiki/Universal_Unique_Identifier)
- Private link, used to remove the file or to check the download counter
- Basic terms of service

Once the expiry date or the download limit is reached, the download is no longer available and the file is deleted.

## Installation
### From packages
Check the [release](https://github.com/epoupon/fileshelter/releases) page to get the latest package for your distribution.

### From Source
#### Debian/Ubuntu dependencies
```sh
$ apt-get install build-essential autoconf automake libboost-dev libwtdbosqlite-dev libwthttp-dev libwtdbo-dev libwt-dev libconfig++-dev
```
#### CentOS 7 dependencies
You need to install [wt](https://www.webtoolkit.eu/wt/doc/reference/html/InstallationUnix.html) from source:
```sh
$ yum groupinstall 'Development Tools'
$ yum install boost-devel
$ git clone https://github.com/emweb/wt.git wt
$ cd wt; mkdir build
$ cmake ../ -DWT_CPP_11_MODE=-std=c++11 -DCMAKE_INSTALL_PREFIX=/usr
$ make install
```
Once this is done, you can install fileshelter's extra dependencies:
```sh
yum install libconfig-devel
```

#### Build
```sh
$ git clone https://github.com/epoupon/fileshelter.git fileshelter
$ cd fileshelter
$ autoreconf -vfi
$ mkdir build
$ cd build
$ ../configure --prefix=/usr --sysconfdir=/etc
```
configure will complain if a mandatory library is missing.

```sh
$ make
```

```sh
$ make install
```
This last command requires root privileges.

## Configuration
FileShelter uses a configuration file, installed in '/etc/fileshelter.conf'
It is recommended to edit this file and change the relevant settings (working directory, maximum file size, maximum validity duration, listen port, etc.)

A basic "Terms of Services" is provided, located in '/usr/share/fileshelter/approot/tos.xml'. You may modify it to fit your needs.
The configuration file contains the definition of the fields needed by this tos.

It is highly recommended to run fileshelter as a non root user. Therefore make sure the user has write permissions on the working directory.

## Running
```sh
$ fileshelter
```
Logs are output in the working directory, in the file 'fileshelter.log'

Alternatively, you may want to specify another configuration file:
```sh
$ fileshelter /another/config/file
```

To connect to FileShelter, just open your favorite browser and go to http://localhost:5091

## Credits
- Wt, awesome framework: http://www.webtoolkit.eu/
- Bootstrap: http://getbootstrap.com/


