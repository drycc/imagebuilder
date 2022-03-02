FROM docker.io/drycc/base:bullseye

ADD . /
ENV PODMAN_VERSION="4.0.1" \
  MC_VERSION="2022.02.26.03.58.31" \
  CADDY_VERSION="2.4.6" \
  PACK_VERSION="0.24.0"

RUN install-packages procps psmisc \
  && install-stack podman $PODMAN_VERSION \
  && install-stack mc $MC_VERSION \
  && install-stack caddy $CADDY_VERSION \
  && install-stack pack $PACK_VERSION \
  && rm -rf \
      /usr/share/doc \
      /usr/share/man \
      /usr/share/info \
      /usr/share/locale \
      /var/lib/apt/lists/* \
      /var/log/* \
      /var/cache/debconf/* \
      /etc/systemd \
      /lib/lsb \
      /lib/udev \
      /usr/lib/`echo $(uname -m)`-linux-gnu/gconv/IBM* \
      /usr/lib/`echo $(uname -m)`-linux-gnu/gconv/EBC* \
  && mkdir -p /usr/share/man/man{1..8}

WORKDIR /app
ENV HOME /tmp
ENV XDG_DATA_HOME /tmp
ENV XDG_CONFIG_HOME /tmp/.config

ENTRYPOINT ["init-stack", "/imagebuilder/build"]

