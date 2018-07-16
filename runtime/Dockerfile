# Release Container
FROM alpine:3.8 as release

ENV MIX_ENV=prod
ENV REPLACE_OS_VARS true
ENV LC_ALL=en_US.UTF-8

ARG AWS_CLI_VERSION=1.15.56
RUN apk --no-cache add \
  bash \
  libcrypto1.0 \
  openssl \
  curl \
  python \
  py-pip \
  jq \
  && pip install --no-cache-dir awscli==$AWS_CLI_VERSION

WORKDIR /app
