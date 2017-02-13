FROM armv7/armhf-ubuntu:14.04
MAINTAINER Sung-Jae Lee <sjlee@mail.com>

# initialize apt-get db & key
RUN DEBIAN_FRONTEND=noninteractive apt-get --fix-missing update 
# dependencies for CoreCLR & CoreFX run
RUN DEBIAN_FRONTEND=noninteractive apt-get -qqy install \
    gettext \
    libicu52 \
    libunwind8
