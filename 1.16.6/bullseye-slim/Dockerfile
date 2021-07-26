FROM debian:bullseye-slim
LABEL maintainer="fillin Inc."
ENV LANG C.UTF-8

ARG GO_VERSION=1.16.6
ARG GO_CHECKSUM=be333ef18b3016e9d7cb7b1ff1fdb0cac800ca0be4cf2290fe613b3d069dfe0d
ARG GO_TAR_NAME=go${GO_VERSION}.linux-amd64.tar.gz
ARG GO_ROOT=/usr/local/go

ADD https://golang.org/dl/${GO_TAR_NAME} /tmp

RUN apt-get -qq update \
      && apt-get install -y git make \
      && echo "${GO_CHECKSUM} /tmp/${GO_TAR_NAME}" > /tmp/checksum.dat \
      && cat /tmp/checksum.dat && sha256sum -c /tmp/checksum.dat \
      && tar xvzf /tmp/${GO_TAR_NAME} -C /tmp \
      && mv /tmp/go /usr/local/ \
      && ln -s ${GO_ROOT}/bin/go /bin/go \
      && rm -rf ${GO_ROOT}/blog ${GO_ROOT}/api ${GO_ROOT}/doc ${GO_ROOT}/test \
      && rm -rf /tmp/* \
      && rm -rf /var/lib/apt/lists/*
