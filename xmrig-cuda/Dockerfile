FROM nvidia/cuda:11.0-devel-ubuntu20.04 as builder

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt -y --no-install-recommends install git \
                                                                          make \
                                                                          cmake \
                                                                          gcc \
                                                                          g++ \
                                                                          libhwloc-dev \
                                                                          libuv1-dev \
                                                                          libssl-dev && \
    apt clean

RUN git clone https://github.com/xmrig/xmrig-cuda.git && \
    mkdir xmrig-cuda/build && \
    cd xmrig-cuda/build && \
    cmake .. && \
    make

RUN git clone https://github.com/xmrig/xmrig.git && \
    sed -i 's/kDefaultDonateLevel = 1/kDefaultDonateLevel = 0/g' xmrig/src/donate.h && \
    sed -i 's/kMinimumDonateLevel = 1/kMinimumDonateLevel = 0/g' xmrig/src/donate.h && \
    mkdir xmrig/build && \
    cd xmrig/build && \
    cmake .. && \ 
    make

RUN mv /xmrig-cuda/build/libxmrig-cuda.so /xmrig/build/libxmrig-cuda.so

FROM nvidia/cuda:11.0-runtime-ubuntu20.04

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt -y --no-install-recommends install libhwloc15 && \
    apt clean

# Linking of nvml
RUN ln -s /usr/lib/x86_64-linux-gnu/libnvidia-ml.so.1 /usr/lib/x86_64-linux-gnu/libnvidia-ml.so

COPY --from=builder /xmrig/build /xmrig
WORKDIR /xmrig

ENTRYPOINT ["./xmrig"]
