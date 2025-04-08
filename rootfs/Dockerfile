ARG CODENAME
FROM registry.drycc.cc/drycc/base:${CODENAME}

ENV DRYCC_UID=1001 \
  DRYCC_GID=1001 \
  DRYCC_HOME_DIR=/home/drycc \
  JQ_VERSION="1.7.1" \
  YQ_VERSION="4.45.1" \
  PODMAN_VERSION="5.4.1" \
  MC_VERSION="2025.04.03.17.07.56" \
  CADDY_VERSION="2.9.1" \
  PACK_VERSION="0.36.4" \
  GOSU_VERSION="1.17"

RUN groupadd drycc --gid ${DRYCC_GID} \
  && useradd drycc -u ${DRYCC_UID} -g ${DRYCC_GID} -s /bin/bash -m -d ${DRYCC_HOME_DIR}

ADD . /

RUN install-packages procps psmisc \
  && install-stack jq $JQ_VERSION \
  && install-stack yq $YQ_VERSION \
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
