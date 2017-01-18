FROM ubuntu:14.04

#
# setup dev env
#

# initialize apt-get db & key
RUN DEBIAN_FRONTEND=noninteractive apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install wget
RUN echo "deb http://llvm.org/apt/trusty/ llvm-toolchain-trusty-3.8 main" | sudo tee /etc/apt/sources.list.d/llvm.list
RUN wget -O - http://llvm.org/apt/llvm-snapshot.gpg.key | sudo apt-key add -
RUN DEBIAN_FRONTEND=noninteractive apt-get update

## install dependencies for coreclr
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y install cmake llvm-3.8 clang-3.8 lldb-3.8 lldb-3.8-dev libunwind8 libunwind8-dev gettext libicu-dev liblttng-ust-dev libcurl4-openssl-dev libssl-dev uuid-dev

## install dependendies for corefx
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y install git clang-3.8 cmake make libc6-dev libssl-dev libkrb5-dev libcurl4-openssl-dev zlib1g-dev
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y install libunwind8 libicu52 curl

## install toolchain for linux-arm target build
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y install gcc-arm-linux-gnueabihf g++-arm-linux-gnueabihf

## install toolchain for linux-armel target build
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y install gcc-arm-linux-gnueabi g++-arm-linux-gnueabi

## install tools for build-rootfs.sh run
#RUN DEBIAN_FRONTEND=noninteractive apt-get -y install qemu binfmt-support qemu-user-static debootstrap

# install dependencies for dotnet arm build
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install llvm-3.8 clang-3.8 lldb-3.8 lldb-3.8-dev cmake make curl gettext git libc6-dev libcurl4-openssl-dev libicu52 libicu-dev libkrb5-dev liblttng-ust-dev libssl-dev libunwind8 libunwind8-dev uuid-dev zlib1g-dev binfmt-support g++-arm-linux-gnueabi gcc-arm-linux-gnueabi g++-arm-linux-gnueabihf gcc-arm-linux-gnueabihf qemu qemu-user-static debootstrap 

RUN useradd -u 1000 -s /bin/bash -m sjlee && passwd -d sjlee && cp /root/.bashrc /home/sjlee && cp /root/.profile /home/sjlee && chown -R sjlee.sjlee /home/sjlee
RUN sed -e "/^sudo:/s/$/sjlee/" /etc/group > /etc/group.new && mv /etc/group.new /etc/group

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
#RUN mv ~/git/coreclr/cross/rootfs/arm ~/arm-rootfs-coreclr

## build coreclr
#RUN ROOTFS_DIR=~/arm-rootfs-coreclr/ time ~/git/coreclr/build.sh arm cross release verbose skiptests clang3.8 cmakeargs -DFEATURE_GDBJIT=TRUE 2>&1 | tee "~/git/coreclr-build-$(date +%m%d-%H%M%S).log"

#
# build corefx-arm
#

## build root file system for arm target build
#RUN ~/git/corefx/cross/build-rootfs.sh arm trusty
#RUN mv ~/git/corefx/cross/rootfs/arm ~/arm-rootfs-corefx

## build corefx
#RUN ROOTFS_DIR=~/arm-rootfs-corefx/ time ~/git/corefx/build-native.sh -release -buildArch=arm -- cross clang3.8 /p:SkipTests=true /p:Outerloop=true /p:TestWithoutNativeImages=true 2>&1 | tee "~/git/corefx-native-build-$(date +%m%d-%H%M%S).log"
#RUN ROOTFS_DIR=~/arm-rootfs-corefx/ time ~/git/corefx/build-managed.sh -release -buildArch=arm -- /p:SkipTests=true /p:Outerloop=true /p:TestWithoutNativeImages=true 2>&1 | tee "~/git/corefx-managed-build-$(date +%m%d-%H%M%S).log"

