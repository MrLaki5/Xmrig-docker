FROM nvidia/cuda:11.0-devel-ubuntu20.04

RUN apt update && \
    DEBIAN_FRONTEND=noninteractive apt -y --no-install-recommends install git \
                                                                          make \
                                                                          cmake \
                                                                          gcc \
                                                                          g++ \
                                                                          libhwloc-dev \
                                                                          libuv1-dev \
                                                                          libssl-dev 

RUN git clone https://github.com/xmrig/xmrig-cuda.git
RUN mkdir xmrig-cuda/build
WORKDIR xmrig-cuda/build
RUN cmake .. && make

WORKDIR ../..
RUN git clone https://github.com/xmrig/xmrig.git
RUN mkdir xmrig/build
WORKDIR xmrig/build
RUN cmake .. && make

RUN mv ../../xmrig-cuda/build/libxmrig-cuda.so .
# Linking of nvml
RUN ln -s /usr/lib/x86_64-linux-gnu/libnvidia-ml.so.1 /usr/lib/x86_64-linux-gnu/libnvidia-ml.so

ENTRYPOINT ["./xmrig"]
