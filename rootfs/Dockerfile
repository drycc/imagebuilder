FROM registry.drycc.cc/drycc/base:bullseye

ENV DRYCC_UID=1001 \
  DRYCC_GID=1001 \
  DRYCC_HOME_DIR=/home/drycc \
  PODMAN_VERSION="4.5.1" \
  MC_VERSION="2022.08.28.20.08.11" \
  CADDY_VERSION="2.6.4" \
  PACK_VERSION="0.29.0" \
  GOSU_VERSION="1.16"

RUN groupadd drycc --gid ${DRYCC_GID} \
  && useradd drycc -u ${DRYCC_UID} -g ${DRYCC_GID} -s /bin/bash -m -d ${DRYCC_HOME_DIR}

ADD . /

RUN install-packages procps psmisc \
  && install-stack podman $PODMAN_VERSION \
  && install-stack mc $MC_VERSION \
  && install-stack caddy $CADDY_VERSION \
  && install-stack pack $PACK_VERSION \
  && install-stack gosu $GOSU_VERSION \
  && usermod --add-subuids 200000-201000 --add-subgids 200000-201000 drycc \
  && chown -R ${DRYCC_UID}:${DRYCC_GID} /opt/drycc \
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

ENTRYPOINT ["init-stack", "/imagebuilder/prebuild", "/imagebuilder/build"]

