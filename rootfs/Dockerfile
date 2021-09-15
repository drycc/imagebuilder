FROM docker.io/minio/mc:latest as mc
FROM docker.io/drycc/go-dev:latest as go-dev

FROM quay.io/containers/podman:latest

ADD . /
COPY --from=mc /usr/bin/mc /bin/mc
COPY --from=go-dev /usr/local/bin/pack /bin/pack

RUN /imagebuilder/install

WORKDIR /app
ENV HOME /tmp
ENV XDG_DATA_HOME /tmp
ENV XDG_CONFIG_HOME /tmp/.config

ENTRYPOINT ["/imagebuilder/build"]