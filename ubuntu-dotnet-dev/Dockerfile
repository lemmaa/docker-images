FROM ubuntu:14.04
MAINTAINER Sung-Jae Lee <sjlee@mail.com>

# initialize apt-get db & key
RUN DEBIAN_FRONTEND=noninteractive apt-get --fix-missing update 
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    curl \
    wget \
    unzip

# dependencies for CoreCLR & CoreFX build
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    build-essential \
    git \
    make \
    cmake \
    gettext \
    libc6-dev \
    libcurl4-openssl-dev \
    libicu52 curl \
    libicu-dev \
    libkrb5-dev \
    liblttng-ust-dev \
    libssl-dev \
    libunwind8 \
    libunwind8-dev \
    uuid-dev \
    zlib1g-dev 

# dependencies for linux-armhf crossbuild
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    binutils-arm-linux-gnueabihf 

# install tools for build-rootfs.sh run
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    qemu \
    binfmt-support \
    qemu-user-static \
    debootstrap 

# add user `dotnet`
RUN useradd -u 1000 -G sudo -s /bin/bash -m dotnet && \
    passwd -d dotnet 

## install prerequisities for llvm-3.8 build
#RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
#    binutils \
#    gcc \
#    g++ \
#    gcc-arm-linux-gnueabihf \
#    g++-arm-linux-gnueabihf \
#    python-dev \
#    zlibc \
#    gzip \
#    bzip2 \
#    xz-utils

## dependencies for tizen-armel crossbuild
#RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
#    binutils-arm-linux-gnueabi \
#    libxml2-utils \
#    rpm2cpio

# install llvm-3.8 toolchain
#RUN echo "deb http://llvm.org/apt/trusty/ llvm-toolchain-trusty-3.8 main" | sudo tee /etc/apt/sources.list.d/llvm.list
#RUN wget -O - http://llvm.org/apt/llvm-snapshot.gpg.key | sudo apt-key add -
#RUN DEBIAN_FRONTEND=noninteractive apt-get update
#RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
#    llvm-3.8 \
#    clang-3.8 \
#    lldb-3.8 \
#    lldb-3.8-dev 

## install toolchain for linux-arm crossbuild
#RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
#    gcc-arm-linux-gnueabihf \
#    g++-arm-linux-gnueabihf \
#    gcc-arm-linux-gnueabi \
#    g++-arm-linux-gnueabi

#
# setup source repo
#

## make git base directory
#RUN mkdir ~/git

## setup coreclr repo & checkout working branch named as today
#RUN git -C ~/git clone https://github.com/lemmaa/coreclr.git
#RUN git -C ~/git/coreclr remote add dotnet https://github.com/dotnet/coreclr.git
#RUN git -C ~/git/coreclr fetch --all
#RUN git -C ~/git/coreclr branch m/$(date +%m%d)
#RUN git -C ~/git/coreclr checkout m/$(date +%m%d)
#RUN git -C ~/git/coreclr merge dotnet/master

## setup corefx repo & checkout working branch named as today
#RUN git -C ~/git clone https://github.com/lemmaa/corefx.git
#RUN git -C ~/git/corefx remote add dotnet https://github.com/dotnet/corefx.git
#RUN git -C ~/git/corefx fetch --all
#RUN git -C ~/git/corefx branch m/$(date +%m%d)
#RUN git -C ~/git/corefx checkout m/$(date +%m%d)
#RUN git -C ~/git/corefx merge dotnet/master

#
# build coreclr-arm
#

## build root file system for arm target build
#RUN ~/git/coreclr/cross/build-rootfs.sh arm trusty lldb3.8
#RUN mv ~/git/coreclr/cross/rootfs/arm ~/rootfs/arm-coreclr

## build coreclr
#RUN time (ROOTFS_DIR=~/rootfs/arm-coreclr/ ~/git/coreclr/build.sh arm cross checked verbose clang3.8 cmakeargs -DFEATURE_GDBJIT=TRUE 2>&1 | tee "../coreclr-build-$(date +%m%d-%H%M%S).log")

#
# build corefx-arm
#

## build root file system for arm target build
#RUN ~/git/corefx/cross/build-rootfs.sh arm trusty
#RUN mv ~/git/corefx/cross/rootfs/arm ~/rootfs/arm-corefx

## build corefx
#RUN time (ROOTFS_DIR=~/rootfs/arm-corefx/ ~/git/corefx/build-native.sh -release -buildArch=arm -- cross clang3.8 /p:SkipTests=true /p:Outerloop=true /p:TestWithoutNativeImages=true 2>&1 | tee "../corefx-native-build-$(date +%m%d-%H%M%S).log")
#RUN time (ROOTFS_DIR=~/rootfs/arm-corefx/ ~/git/corefx/build-managed.sh -release -buildArch=arm -- /p:SkipTests=true /p:Outerloop=true /p:TestWithoutNativeImages=true 2>&1 | tee "../corefx-managed-build-$(date +%m%d-%H%M%S).log")

