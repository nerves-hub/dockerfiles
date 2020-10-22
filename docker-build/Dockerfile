FROM alpine:3.12.0

ARG AWS_CLI_VERSION=1.18.162

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
