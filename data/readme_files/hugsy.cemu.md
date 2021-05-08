# CEMU #

[![MIT](https://img.shields.io/packagist/l/doctrine/orm.svg?maxAge=2592000?style=plastic)](https://github.com/hugsy/cemu/blob/master/LICENSE) [![IRC](https://img.shields.io/badge/freenode-%23%23cemu-yellowgreen.svg)](https://webchat.freenode.net/?channels=##cemu) [![Python-Version](https://img.shields.io/pypi/pyversions/cemu.svg)](https://pypi.python.org/pypi/cemu) [![PyPi-Version](https://img.shields.io/pypi/v/cemu.svg)](https://pypi.python.org/pypi/cemu) [![Downloads](https://pepy.tech/badge/cemu)](https://pepy.tech/project/cemu)

![cemu-linux](https://i.imgur.com/iHtWvTL.png)


## Description ##


Writing assembly is fun. Assembly is the lowest language (humanly
understandable) available to communicate with computers, and is crucial
to understand the internal mechanisms of any machine. Unfortunately,
setting up an environment to write, compile and run assembly for various
architectures (x86, ARM, MIPS, SPARC) has always been painful. **CEmu**
is an attempt to fix this by providing a bundled GUI application that
empowers users to write assembly and test it by compiling it to bytecode
and executing it in an QEMU-based emulator.

**CEmu** combines all the advantages of a basic assembly IDE,
compilation and execution environment, by relying on the great libraries
[Keystone](https://github.com/keystone-engine/keystone),
[Unicorn](https://github.com/unicorn-engine/unicorn/) and
[Capstone](https://github.com/aquynh/capstone) engines in a Qt powered
GUI.

It allows to test binary samples, check your shellcodes or even simply
learn how to write assembly code, all of this for the following
architectures:

  - x86-32 / x86-64
  - Arm / AArch64
  - MIPS / MIPS64
  - SPARC / SPARC64
  - (more to come)

`CEmu` was tested and works on Linux, Windows and MacOSX.


## Installation ##

Since version 0.2.2, `cemu` is now Python3 only for simplicity (and also due to
the fact that [Python2 will soon cease to exist](https://pythonclock.org/)).

If your current installation of `cemu` is <= 0.2.1 and on Python2, please
uninstall it and install it using Python3.


### Quick install with PIP ###

Last stable from PyPI:

```bash
pip3 install cemu
```

Last stable from Github:

```bash
git clone https://github.com/hugsy/cemu && cd cemu
pip3 install --upgrade .
```

For 99% of cases, that's all you need to do. `cemu` will be installed in your `${LOCALPATH}/bin` directory (by default, `/usr/local/bin/cemu` if installed as root, `~/.local/bin/cemu` for non-root).


### Installation notes ###

#### Kali Linux ####

If you are using Kali Linux, there is a [known problem](https://github.com/keystone-engine/keystone/issues/235)
with the installation of the `keystone-engine` package using PIP. A quick'n dirty fix for that would be (as `root`):

```bash
$ sudo updatedb
$ sudo locate libkeystone.so
$ sudo ln -sf /path/to/libkeystone.so/found/above /usr/local/lib/libkeystone.so
```

#### OSX ####

If you are using OSX, I would highly recommand installing Capstone engine directly using `brew.sh` command instead of `pip`, as its version seems more up-to-date than the one on PyPI. Doing so, the installation should work out of the box:

```bash
$ brew install capstone
$ pip3 install -U cemu
```

#### Windows ####

The fastest way for Windows is to install the packaged binaries for:

  - Keystone (http://www.keystone-engine.org/download/)
    - Including the [Microsoft VC++ runtime library](https://www.microsoft.com/en-gb/download/details.aspx?id=40784)
  - Capstone (http://www.capstone-engine.org/download.html)
  - Unicorn (http://www.unicorn-engine.org/download/)


Then spawn `cmd.exe` and install the missing Python packages using `pip`:

```bash
# From PyPI
C:\> pip.exe install -U cemu
# From Github
## Download ZIP and extract it
C:\> cd path\to\cemu
C:\path\to\cemu> pip.exe install . -U
```

`CEmu` launcher (`cemu.exe`) will be in the `C:\Python3\Scripts` directory.


## Contribution ##

`cemu` was created and maintained by myself, [`@_hugsy_`](https://twitter.com/_hugsy_), but kept fresh thanks to
all the [contributors](https://github.com/hugsy/cemu/graphs/contributors).
