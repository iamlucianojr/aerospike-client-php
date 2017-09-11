# Aerospike PHP Client
[![Build Status](https://travis-ci.org/aerospike/aerospike-client-php.svg?branch=master)](https://travis-ci.org/aerospike/aerospike-client-php)
[![Latest Release](https://img.shields.io/packagist/v/aerospike/aerospike-client-php.svg)](https://img.shields.io/packagist/v/aerospike/aerospike-client-php.svg)
[![Downloads](https://img.shields.io/packagist/dt/aerospike/aerospike-client-php.svg)](https://img.shields.io/packagist/dt/aerospike/aerospike-client-php.svg)
[![License](https://img.shields.io/packagist/l/aerospike/aerospike-client-php.svg)](https://img.shields.io/packagist/l/aerospike/aerospike-client-php.svg)

## Version support

Note: This client supports PHP versions 5.3.3+, 5.4, 5.5, 5.6. If you are looking for an Aerospike client which supports PHP7, it can be found at the [aerospike-client-php repo](https://github.com/aerospike/aerospike-client-php).

The PHP extension was tested to build on 64-bit

 - Ubuntu 12.04 LTS, 14.04 LTS, Debian 7, 8 and related distros using the **apt** package manager
 - CentOS 6.x, 7.x, RedHat 6.x, 7.x and related distros using the **yum** package manager
 - OS X 10.9 (Mavericks), 10.10 (Yosemite)

Windows is currently not supported.

## Documentation

Documentation of the Aerospike PHP Client may be found in the [doc directory](doc/README.md).
The API described there is the [specification](doc/aerospike.md) for the PHP Client.
Notes on the internals of the implementation are in [doc/internals.md](doc/internals.md).

[Example PHP code](examples/) can be found in the `examples/` directory.

Full documentation of the Aerospike database is available at http://www.aerospike.com/docs/

## Dependencies

### CentOS and RedHat (yum)

    sudo yum groupinstall "Development Tools"
    sudo yum install openssl-devel
    sudo yum install php-devel php-pear # unless PHP was manually installed

### Ubuntu and Debian (apt)

    sudo apt-get install build-essential autoconf libssl-dev
    sudo apt-get install php5-dev php-pear # unless PHP was manually installed

### OS X

By default OS X will be missing command line tools. On Mavericks (OS X 10.9)
and higher those [can be installed without Xcode](http://osxdaily.com/2014/02/12/install-command-line-tools-mac-os-x/).

    xcode-select --install # install the command line tools, if missing

The dependencies can be installed through the OS X package manager [Homebrew](http://brew.sh/).

    brew update && brew doctor
    brew install automake
    brew install openssl

To switch PHP versions [see this gist](https://gist.github.com/rbotzer/198a04f2315e88c75322).

## Installation

### Building with Composer

Using [Composer](https://getcomposer.org/) you can download and build the PHP
extension:

    composer require aerospike/aerospike-client-php5 "~3.4"
    find vendor/aerospike/aerospike-client-php/ -name "*.sh" -exec chmod +x {} \;
    cd vendor/aerospike/aerospike-client-php/ && sudo composer run-script post-install-cmd

### Building Manually

To build the PHP extension manually you will need to fetch the
[latest release](https://github.com/aerospike/aerospike-client-php/releases/latest)
from Github, then run the `build.sh` script in the `src/aerospike/` directory.

    cd src/aerospike
    ./build.sh

This will download the Aerospike C client SDK if necessary into
`src/aerospike-client-c/`, and initiate `make`.

## Installing the PHP Extension

To install the PHP extension do:

    make install
    php -i | grep ".ini "

Now edit the php.ini file.  If PHP is configured --with-config-file-scan-dir
(usually set to `/etc/php.d/`) you can create an `aerospike.ini` file in the
directory, otherwise edit `php.ini` directly. Add the following directive:

    extension=aerospike.so
    aerospike.udf.lua_system_path=/path/to/aerospike/lua
    aerospike.udf.lua_user_path=/path/to/aerospike/usr-lua

The *aerospike* module should now be available to the PHP CLI:

    php -m | grep aerospike
    aerospike

Remember that if you are using PHP with Nginx or Apache there is likely a
separate `php.ini` config file for the web server  Copy the `aerospike.ini`
you have just created into `/etc/php5/apache2/conf.d/`, `/etc/php5/fpm/conf.d/`
or wherever the configuration include directory of the web server is, then issue
a graceful restart.

## License

The Aerospike PHP Client is made availabled under the terms of
the Apache License, Version 2, as stated in the file [LICENSE](./LICENSE).

Individual files may be made available under their own specific license,
all compatible with Apache License, Version 2. Please see individual files for
details.


