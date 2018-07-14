FROM alpine:3.8 as build

ARG FWUP_VERSION
ENV FWUP_VERSION=${FWUP_VERSION}

# Add build tools
RUN apk add --no-cache \
  linux-headers \
  gcc \
  musl-dev \
  autoconf \
  automake \
  libtool \
  curl \
  make \
  libarchive-dev \
  confuse-dev \
  libsodium-dev

# Add tools needed for testing
RUN apk add --no-cache \
  dosfstools \
  mtools \
  zip \
  unzip

RUN addgroup -g 1000 fwup && \
    adduser -D -u 1000 -G fwup fwup

USER fwup
WORKDIR /home/fwup

RUN curl -sL https://github.com/fhunleth/fwup/archive/v$FWUP_VERSION.tar.gz | tar xz \
  && mv fwup-$FWUP_VERSION fwup

WORKDIR /home/fwup/fwup

RUN \
  ./autogen.sh \
  && PKG_CONFIG_PATH=./build/host/deps/usr/lib/pkgconfig ./configure --enable-shared=no

RUN make
RUN make check
USER root
RUN make install

FROM alpine:3.8
COPY --from=build /usr/local/bin/fwup /usr/local/bin/fwup
