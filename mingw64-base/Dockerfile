FROM archlinux/base

RUN pacman --noconfirm -Syy
RUN pacman --noconfirm -S tar \
    sudo \
    grep \
    binutils \
    make \
    file \
    fakeroot \
    gcc \
    awk \
    patch \
    m4 \
    diffutils \
    automake \
    autoconf \
    which

RUN useradd builduser -m \
    && passwd -d builduser \
    && printf 'builduser ALL=(ALL) ALL\n' | tee -a /etc/sudoers

USER builduser

RUN cd \
    && curl -L https://aur.archlinux.org/cgit/aur.git/snapshot/yay.tar.gz -o yay.tar.gz \
    && tar xvf yay.tar.gz \
    && cd yay \
    && makepkg --noconfirm -si


RUN yay --noconfirm -S mingw-w64-binutils-bin
RUN yay --noconfirm -S mingw-w64-headers-bin
RUN yay --noconfirm -S mingw-w64-crt-bin
RUN yay --noconfirm -S mingw-w64-winpthreads-bin
RUN yay --noconfirm -S mingw-w64-gcc-bin
RUN yay --noconfirm -S mingw-w64-cmake

USER root
RUN userdel -r builduser
