# xmrig-docker
Docker containers for xmrig-cpu and xmrig-cuda gpu miners

## Build image
### xmrig cpu
``` bash
docker build ./xmrig -t xmrig-docker
```

### xmrig-cuda gpu
Note: For cuda docker image Nvidia-docker 2.0 is required. [install](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html).
``` bash
docker build ./xmrig-cuda -t xmrig-cuda-docker
```

## Run
### xmrig cpu
``` bash
docker run --rm xmrig-docker -o <url of mining server>:<port> -u <wallet address> -p <device name>
```

### xmrig-cuda gpu
``` bash
docker run --rm xmrig-cuda-docker -o <url of mining server>:<port> -u <wallet address> -p <device name> --cuda
```
