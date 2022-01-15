ARG ALPINE_VERSION=3.15.0

FROM alpine:${ALPINE_VERSION}

RUN apk add --no-cache git \
                       make \
                       cmake \
                       libstdc++ \
                       gcc \
                       g++ \
                       hwloc-dev \
                       libuv-dev \
                       openssl-dev 

RUN git clone https://github.com/xmrig/xmrig.git
RUN mkdir xmrig/build
WORKDIR xmrig/build
RUN cmake .. && make

ENTRYPOINT ["./xmrig"]
