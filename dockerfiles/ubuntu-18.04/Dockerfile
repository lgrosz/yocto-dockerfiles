# ubuntu-18.04-base
# Copyright (C) 2015-2021 Intel Corporation
#
# SPDX-License-Identifier: GPL-2.0-only
#

FROM ubuntu:18.04

ARG TARGETPLATFORM

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y \
        build-essential \
        chrpath \
        cpio \
        debianutils \
        diffstat \
        gawk \
        git-core \
        iputils-ping \
        libegl1-mesa \
        libsdl1.2-dev \
        locales \
        pylint3 \
        python \
        python3 \
        python3-git \
        python3-jinja2 \
        python3-pexpect \
        python3-pip \
        rsync \
        socat \
        sudo \
        texinfo \
        unzip \
        wget \
        xterm \
        xz-utils  \
        zstd && \
    case ${TARGETPLATFORM} in \
        "linux/amd64") \
            DEBIAN_FRONTEND=noninteractive apt-get install -y \
                gcc-multilib \
                g++-multilib \
            ;; \
    esac && \
    useradd -U -m yoctouser && \
    /usr/sbin/locale-gen en_US.UTF-8 && \
    echo 'dash dash/sh boolean false' | debconf-set-selections && \
    DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

COPY build-install-dumb-init.sh /
RUN  bash /build-install-dumb-init.sh && \
     rm /build-install-dumb-init.sh && \
     apt-get clean

USER yoctouser
WORKDIR /home/yoctouser
CMD /bin/bash
