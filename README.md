# VTS-Registry

[VTS-Registry](https://github.com/melown/vts-registry) is basic database of
input configuration values, such as data credits (or data attributions), basic
bound layers, reference frames and other data.

## User documentation

VTS-Registry user documentation is available at
https://melown.readthedocs.io/


## Download, build and install

### Clone and Download

The source code can be donwloaded from
[GitHub repository](https://github.com/melown/vts-registry), but since there are
external dependences, you have to use `--recursive` switch while cloning the
repo.


```
git clone --recursive https://github.com/Melown/vts-registry.git 
```

**NOTE:** If you did clone from GitHub previously without the `--recursive`
parameter, you should probably delete the `vts-mapproxy` directory and clone
again. The build will not work otherwice.

### Build

For building VTS-Registry, you just have to use ``make``

```
cd vts-registry/registry/
make
```

The `deb` package is stored in root directory and you can install it system-wide

```
sudo dpkg -i ../vts-registry_1.0_amd64.deb
```

## Install from Melown repository

We provide precompiled packages for some popular linux distributions. See [Melown OSS package repository
](http://cdn.melown.com/packages/) for more information. This repository contains all needed packages to run
VTS OSS software.

## How to contribute

Check the [CONTRIBUTING.md](CONTRIBUTING.md) file.
