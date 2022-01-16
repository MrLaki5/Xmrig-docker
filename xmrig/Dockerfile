ARG ALPINE_VERSION=3.15.0

FROM alpine:${ALPINE_VERSION} as builder

RUN apk add --no-cache git \
                       make \
                       cmake \
                       libstdc++ \
                       gcc \
                       g++ \
                       hwloc-dev \
                       libuv-dev \
                       openssl-dev 

RUN git clone https://github.com/xmrig/xmrig.git && \
    sed -i 's/kDefaultDonateLevel = 1/kDefaultDonateLevel = 0/g' xmrig/src/donate.h && \
    sed -i 's/kMinimumDonateLevel = 1/kMinimumDonateLevel = 0/g' xmrig/src/donate.h && \
    mkdir xmrig/build && \
    cd xmrig/build && \
    cmake .. && \
    make

FROM alpine:${ALPINE_VERSION}

RUN apk add --no-cache hwloc \
                       libuv

COPY --from=builder /xmrig/build/xmrig /xmrig/xmrig
WORKDIR /xmrig

ENTRYPOINT ["./xmrig"]
