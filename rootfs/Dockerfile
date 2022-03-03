FROM docker.io/drycc/base:bullseye

RUN adduser --system \
  --shell /bin/bash \
  --disabled-password \
  --home /workspace \
  --group drycc

ADD . /
ENV PODMAN_VERSION="4.0.2" \
  MC_VERSION="2022.02.26.03.58.31" \
  CADDY_VERSION="2.4.6" \
  PACK_VERSION="0.24.0" \
  GOSU_VERSION="1.14"

RUN install-packages procps psmisc \
  && install-stack podman $PODMAN_VERSION \
  && install-stack mc $MC_VERSION \
  && install-stack caddy $CADDY_VERSION \
  && install-stack pack $PACK_VERSION \
  && install-stack gosu $GOSU_VERSION \
  && usermod --add-subuids 200000-201000 --add-subgids 200000-201000 drycc \
  && chown -R drycc:drycc /opt/drycc/podman \
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

WORKDIR /workspace
ENV HOME /tmp
ENV XDG_DATA_HOME /tmp
ENV XDG_CONFIG_HOME /tmp/.config

ENTRYPOINT ["init-stack", "/imagebuilder/prebuild", "/imagebuilder/build"]

