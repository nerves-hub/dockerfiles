# Release Container
FROM alpine:3.8 as release

ENV MIX_ENV=prod
ENV REPLACE_OS_VARS true
ENV LC_ALL=en_US.UTF-8
ENV AWS_ENV_SHA=1393537837dc67d237a9a31c8b4d3dd994022d65e99c1c1e1968edc347aae63f

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

# Add SSM Parameter Store helper, which is used in the entrypoint script to set secrets
RUN wget https://raw.githubusercontent.com/nerves-hub/aws-env/master/bin/aws-env-linux-amd64 && \
    echo "$AWS_ENV_SHA  aws-env-linux-amd64" | sha256sum -c - && \
    mv aws-env-linux-amd64 /bin/aws-env && \
    chmod +x /bin/aws-env

WORKDIR /app
