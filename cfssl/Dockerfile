FROM golang:alpine as build

ARG CFSSL_VERSION
ENV CFSSL_VERSION=${CFSSL_VERSION}

RUN apk add --no-cache \
  git \
  gcc \
  musl-dev

RUN \
  git clone "https://github.com/cloudflare/cfssl.git" "${GOPATH}/src/github.com/cloudflare/cfssl" \
  && cd "${GOPATH}/src/github.com/cloudflare/cfssl" \
  && git checkout tags/$CFSSL_VERSION

WORKDIR "${GOPATH}/src/github.com/cloudflare/cfssl"

RUN \
  go build -o /usr/local/bin/cfssl ./cmd/cfssl \
  && go build -o /usr/local/bin/cfssljson ./cmd/cfssljson \
  && go build -o /usr/local/bin/mkbundle ./cmd/mkbundle \
  && go build -o /usr/local/bin/multirootca ./cmd/multirootca

FROM alpine:3.8
COPY --from=build /usr/local/bin/cfssl /usr/local/bin/cfssl
COPY --from=build /usr/local/bin/cfssljson /usr/local/bin/cfssljson
COPY --from=build /usr/local/bin/mkbundle /usr/local/bin/mkbundle
COPY --from=build /usr/local/bin/multirootca /usr/local/bin/multirootca
