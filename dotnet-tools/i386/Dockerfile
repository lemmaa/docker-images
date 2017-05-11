FROM ioft/i386-ubuntu:14.04
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

# prepare llvm-3.9 install
RUN wget -O - http://apt.llvm.org/llvm-snapshot.gpg.key | sudo apt-key add -
RUN echo "deb http://apt.llvm.org/trusty/ llvm-toolchain-trusty-3.9 main" >> /etc/apt/sources.list
RUN echo "deb-src http://apt.llvm.org/trusty/ llvm-toolchain-trusty-3.9 main" >> /etc/apt/sources.list
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy update
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    llvm-3.9 \
    clang-3.9 \
    lldb-3.9 \
    lldb-3.8-dev 

# install tools for build-rootfs.sh for tizen run
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    binutils-arm-linux-gnueabi \
    libxml2-utils \
    rpm2cpio

# upgrade vim packages
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy upgrade vim

# install miscellaneous packages
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install bc

# add user `dotnet`
ARG UID=1111
ARG UNAME=dotnet
RUN useradd -u $UID -G sudo -s /bin/bash -m $UNAME && \
    passwd -d $UNAME
WORKDIR /home/$UNAME

