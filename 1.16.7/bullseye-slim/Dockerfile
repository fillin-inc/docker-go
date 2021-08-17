FROM debian:bullseye-slim
LABEL maintainer="fillin Inc."
ENV LANG C.UTF-8

ARG GO_VERSION=1.16.7
ARG GO_CHECKSUM=7fe7a73f55ba3e2285da36f8b085e5c0159e9564ef5f63ee0ed6b818ade8ef04
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
