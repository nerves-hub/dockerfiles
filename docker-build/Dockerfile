FROM alpine:3.8

ARG AWS_CLI_VERSION=1.15.56

ENV BASH_ENV=/etc/profile

RUN apk add --no-cache \
  bash \
  docker \
  curl \
  git \
  openssh \
  python \
  py-pip \
  jq \
  && pip install --no-cache-dir awscli==$AWS_CLI_VERSION

RUN curl -o /usr/local/bin/ecs-deploy \
      https://raw.githubusercontent.com/nerves-hub/ecs-deploy/develop/ecs-deploy \
    && chmod +x /usr/local/bin/ecs-deploy  

CMD ["bash"]
