---
layout: post
title: Install caffe-GPU on Ubuntu-16.04
excerpt: "caffe-GPU with CUDA-8.0, cuDNN v6.0"
categories: [Tutorials]
comments: true
---

In this tutorial we install the Caffe version 1.0.0-rc5 from
[source](https://github.com/BVLC/caffe) (check the Makefile for the Caffe
version).

# <i class="fa fa-desktop"></i> Hardware and OS

## Hardware
```
CPU: Intel(R) Core(TM) i7-5960X CPU @ 3.00GHz
GPU: NVIDIA GeForce GTX 980
```
## OS
```
LSB Version:	core-9.20160110ubuntu0.2-amd64:core-9.20160110ubuntu0.2-noarch:printing-9.20160110ubuntu0.2-amd64:printing-9.20160110ubuntu0.2-noarch:security-9.20160110ubuntu0.2-amd64:security-9.20160110ubuntu0.2-noarch
Distributor ID:	Ubuntu
Description:	Ubuntu 16.04.1 LTS
Release:	16.04
Codename:	xenial
```

# Environment

## Compiler and python environment

Remove anaconda path from `$PATH` (we haven't been able to build with anaconda).
Make sure we have `gcc-5` and `g++-5`.
```
$ echo $PATH  # Should not contain anaconda
$ gcc --version  # 5.4.0
$ g++ --version  # 5.4.0
$ which python   # /usr/bin/python
```

## Install Nvidia driver, cuda-8.0 and cudnn

`nvidia-375` is the latest driver as of March 2017.
```
$ sudo apt-get install nvidia-375
```
Download `cuda-8.0` from Nvidia's site:
[runfile](https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run). Change directory to the downloaded file and run with `sudo`
(filename might be different).
```
$ cd ~/Download
$ sudo sh cuda_8.0.61_375.26_linux.run
```
After installation, run `nvcc --version` to quickly check if everything works so far.
Sign-up for an Nvidia Developer accound and download `cuDNN-v6.0`. Extract the
downloaded file and copy the contents to the corresponding `cuda-8.0` folder.
```
$ sudo cp cudnn/cudnn.h /usr/local/cuda-8.0/include/
$ sudo cp cudnn/libcudnn* /usr/local/cuda-8.0/lib64/
```

## Install build tools

We use Python2.7 in this tutorial.
```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install build-essential cmake git pkg-config
sudo apt-get install libleveldb-dev libsnappy-dev libhdf5-serial-dev
sudo apt-get install libatlas-base-dev
sudo apt-get install --no-install-recommends libboost-all-dev
sudo apt-get install libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install python-dev  # Python 2.7
sudo apt-get install python-numpy python-scipy
sudo apt-get install libopencv-dev
```
We build `protobuf-3.2.0` from
[source](https://github.com/google/protobuf/archive/v3.2.0.tar.gz).
Extract the downloaded tarball and `cd` to the extracted folder.
```
$ sudo apt-get install autoconf automake libtool curl make unzip
$ ./autogen.sh
$ ./configure --prefix=/usr/local/ CC=/usr/bin/gcc
$ make
$ make check
$ sudo make install
$ sudo ldconfig  # refresh shared library cache
```
Note: Add `-j8` flag to `make` for 8 compile jobs running. Check the installation:
```
$ protoc --version
```

## Download Caffe source code

```
$ sudo apt-get install git  # Run this if git is not installed
$ sudo apt-get install vim  # Run this if vim is not installed (optional)
$ git clone https://github.com/BVLC/caffe
```

# Build

## Setting up Makefile.configure

```
$ cd caffe
$ cp Makefile.config.example Makefile.config
$ vim Makefile.config  # Replace vim by any text editor
```
For GPU build, make sure these fields are correct in `Makefile.config`:
```
USE_CUDNN := 1
CUDA_DIR := /usr/local/cuda
CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \
        -gencode arch=compute_20,code=sm_21 \
        -gencode arch=compute_30,code=sm_30 \
        -gencode arch=compute_35,code=sm_35 \
        -gencode arch=compute_50,code=sm_50 \
        -gencode arch=compute_52,code=sm_52 \
        -gencode arch=compute_60,code=sm_60 \
        -gencode arch=compute_61,code=sm_61 \
        -gencode arch=compute_61,code=compute_61
BLAS := atlas
PYTHON_INCLUDE := /usr/include/python2.7 \
                /usr/lib/python2.7/dist-packages/numpy/core/include \
                /usr/local/lib/python2.7/dist-packages/numpy/core/include
PYTHON_LIB := /usr/lib
WITH_PYTHON_LAYER := 1
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/
BUILD_DIR := build
DISTRIBUTE_DIR := distribute
TEST_GPUID := 0
Q ?= @
```
Create symbolic links for `hdf5`:
```
$ cd /usr/lib/x86_64-linux-gnu
$ sudo ln -s libhdf5_serial.so.8.0.2 libhdf5.so
$ sudo ln -s libhdf5_serial_hl.so.8.0.2 libhdf5_hl.so
```

## Run build

```
$ make all -j8
$ make test
$ make runtest
```

## Possible Errors

TODO: protobuf version
TODO: gcc version (CUDA8.0)

# References

http://christopher5106.github.io/big/data/2015/07/16/deep-learning-install-caffe-cudnn-cuda-for-digits-python-on-ubuntu-14-04.html

https://github.com/google/protobuf/blob/master/src/README.md

https://github.com/intel/caffe/wiki/Ubuntu-16.04-or-15.10-Installation-Guide
