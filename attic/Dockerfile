# docker image used to build cfengine AUR package
FROM nubs/arch-build

USER root

RUN pacman --refresh --sync --noconfirm --noprogressbar base-devel
RUN pacman --sync --sysupgrade --noconfirm --noprogressbar
RUN pacman --sync --noconfirm --noprogressbar  lmdb libxml2

USER build
