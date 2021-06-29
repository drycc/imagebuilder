FROM docker.io/minio/mc:latest as mc

FROM docker.io/drycc/go-dev

ADD . /
COPY --from=mc /usr/bin/mc /bin/mc

RUN /imagebuilder/install

WORKDIR /app
ENV HOME /app

#ENTRYPOINT ["/imagebuilder/build"]