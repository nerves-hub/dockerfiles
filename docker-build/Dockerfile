FROM alpine:3.15.6

ARG AWS_CLI_VERSION=1.22.81

ENV BASH_ENV=/etc/profile

RUN apk add --no-cache \
  bash \
  docker \
  curl \
  git \
  openssh \
  python3 \
  py-pip \
  jq \
  && pip install --no-cache-dir awscli==$AWS_CLI_VERSION

RUN curl -o /usr/local/bin/ecs-deploy \
      https://raw.githubusercontent.com/ecs-deploy/ecs-deploy-1/develop/ecs-deploy \
    && chmod +x /usr/local/bin/ecs-deploy

CMD ["bash"]
