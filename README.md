<br />
<p align="center">
  <a href="https://github.com/VedantParanjape/simpPRU">
    <img src="assets/default-monochrome-black.svg" alt="Logo" width="400" height="100">
  </a>

  <p align="center">
    Intuitive language for PRU which compiles down to PRU Assembly.
    <br/>
    <br/>
    <a href="https://simppru.readthedocs.io/en/latest/"><strong>Explore the docs »</strong></a>
    <br />
    <a href="https://github.com/VedantParanjape/simpPRU/issues">Report Bug</a>
    ·
    <a href="https://github.com/VedantParanjape/simpPRU/issues">Request Feature</a>
    ·
    <a href="https://github.com/VedantParanjape/simpPRU/pulls">Send a Pull Request</a>
  </p>
</p>

<p align="center">
<img src="https://github.com/VedantParanjape/simpPRU/workflows/.github/workflows/amd64.yml/badge.svg?branch=master">
<img src="https://github.com/VedantParanjape/simpPRU/workflows/.github/workflows/arm32.yml/badge.svg?branch=master">
<img src="https://img.shields.io/github/stars/VedantParanjape/simpPRU">
<img src="https://img.shields.io/github/forks/VedantParanjape/simpPRU">
<img src="https://img.shields.io/github/issues/VedantParanjape/simpPRU">
<img src="https://img.shields.io/github/repo-size/VedantParanjape/simpPRU">
<img src="https://img.shields.io/github/license/VedantParanjape/simpPRU">
</p>

## Details

***GSoC 2020*** project under BeagleBoard.org

* Name: Vedant Paranjape
* Wiki: <https://elinux.org/BeagleBoard/GSoC/2020_Projects/PRU_Improvements>
* Progress log: <https://ve0x10.me/gsoc2020/>
* Mentors: Abhishek Kumar, Pratim Ugale, Andrew Henderson  
* Organisation: BeagleBoard.org

## Build

Requirements:

* flex
* bison
* gcc
* gcc-pru
* cmake

```bash
mkdir build
cd build
cmake ..
make 
sudo make install

# build debian package
sudo make package

# install debian package
sudo dpkg -i <debian_package_name>.deb
```

## Install

Download debian package from Releases, available for amd64 and arm32 arch

```bash
sudo dpkg -i <debian_package_name>.deb
```

Check `/examples` for different examples

## To Do List

* [ ] Add support for using PWM using eCAP module.
* [ ] Better error handler in bison parser.
* [ ] Update grammar such that control statements (break/continue) can only be called inside loops.
* [ ] Update grammar such that return statements can be called anywhere inside function definitions and not only at the end.
* [ ] Add support for directly calling C code in simppru.
* [ ] Add unit tests which run using pru-sim.
