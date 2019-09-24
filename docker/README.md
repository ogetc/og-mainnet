# 使用docker启动 ogetc

## 环境准备

- 安装 docker
- 安装 docker-compose

## 文件准备

```
.
├── config
│   ├── config.ini
│   └── genesis.json
├── docker-compose.yaml
└── init.yaml
```

- config.ini 是节点配置文件，主要需要修改p2p节点地址和公私钥
- genesis.json 是初始文件
- docker-compose.yaml 是正常启动的配置文件
- init.yaml 是初次启动的配置文件
  
### yaml 文件说明

```
version: "3"

services:
  ogetc:
    image: ogetclab/ogetc:latest
    command: nodeos --data-dir /opt/ogetc/data --config-dir /opt/ogetc/config
    hostname: ogetc
    ports:
      - 8888:8888
      - 9876:9876
    volumes:
      - /data/ogetc/testnet/data:/opt/ogetc/data
      - /data/ogetc/testnet/config:/opt/ogetc/config
```

配置中 /data/ogetc/testnet 需要改成实际机器存放ogetc数据的路径，两个yaml文件都需要修改

## 运行指令

在目录下运行：

- 初次启动 docker-compose -f init.yaml up -d
- 停止服务 docker-compose down
- 停止后重启 docker-compose up -d