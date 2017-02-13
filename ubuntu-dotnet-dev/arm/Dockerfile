FROM armv7/armhf-ubuntu:14.04
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
    libicu52 \
    libicu-dev \
    libkrb5-dev \
    liblttng-ust-dev \
    libssl-dev \
    libunwind8 \
    libunwind8-dev \
    uuid-dev \
    zlib1g-dev 

# add user `dotnet`
RUN useradd -u 1000 -G sudo -s /bin/bash -m dotnet && \
    passwd -d dotnet 
