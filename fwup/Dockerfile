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
  make

# Add runtime tools
RUN apk add --no-cache \
  dosfstools \
  mtools \
  zip \
  unzip

RUN curl -sL https://github.com/fhunleth/fwup/archive/v$FWUP_VERSION.tar.gz | tar xz \
  && mv fwup-$FWUP_VERSION fwup

WORKDIR /fwup

RUN \
  ./scripts/download_deps.sh \
  && ./scripts/build_deps.sh \
  && ./autogen.sh \
  && PKG_CONFIG_PATH=./build/host/deps/usr/lib/pkgconfig ./configure --enable-shared=no

RUN make
#RUN make check
RUN make install

FROM alpine:3.8
COPY --from=build /usr/local/bin/fwup /usr/local/bin/fwup
