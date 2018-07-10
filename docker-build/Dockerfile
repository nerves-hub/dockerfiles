FROM debian:buster-slim

RUN \
    apt-get update -y -qq \
    && apt-get install -y \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     awscli \
     jq \
     software-properties-common \
    && curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
    && add-apt-repository \
      "deb [arch=amd64] https://download.docker.com/linux/debian \
      $(lsb_release -cs) \
      stable" \
    && apt-get update -y -qq \
    && apt-get install -y \
      docker-ce
    
CMD ["bash"]
