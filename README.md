# ![图片描述...](https://img.shields.io/badge/docs-passing-success) Mac、Win 系统一键快速搭建部署集成环境 （Docker、Docker-compose、宝塔）

## 使用操作

下载 `docker` 软件

下载地址参考: http://get.daocloud.io/

## 快速开始

如遇到下载失败，请参考: https://gitclone.com/

    git clone https://github.com/surest-sky/docker-compose-baota.git docker-compose-baota
    cd docker-compose-baota
    docker-compose up -d

### 配置环境

打开 `.env` 文件
修改里面的项目目录地址，这个地址会映射到 对应服务器 `wwwroot` 位置

### 命令

1、启动

    # 启动并后台运行 `-d` 表示后台运行
    docker-compose up -d

2、重启

    # 重启
    docker-compose restart

3、指定每个容器重启

    # container_name 表示 yml 中的容器名称
    docker-compose container_name up -d

    # 这里可以这样使用
    docker-compose bt up -d

4、进入容器环境

    # 查看当前容器ID
    ➜  docker ps
    CONTAINER ID   IMAGE         COMMAND                  CREATED             STATUS                       PORTS                                                                                                                       NAMES
    19cfc43b7a45   pch18/baota   "/bin/sh -c /entrypo…"   About an hour ago   Up About an hour (healthy)   0.0.0.0:80->80/tcp, 0.0.0.0:443->443/tcp, 0.0.0.0:888->888/tcp, 0.0.0.0:3306->3306/tcp, 20-21/tcp, 0.0.0.0:8888->8888/tcp   bt

    # 进入容器
    docker-compose exec 19cfc43b7a45 bash

### 常见问题

- 端口被占用

请检查本地端口是否被使用, 当前容器使用的端口见 `yml` 文件

    ...
    ports: 
      - "80:80"
      - "443:443"
      - "8888:8888"
      - "888:888"
      - "3306:3306"

- 容器下载失败

请检查当前`docker`容器，配置的是否为国内地址

![图片描述...](https://cdn.surest.cn/Frop9zSUUJ4WO1HRqOQXqmLsmOLa)
    {
        "experimental": false,
        "features": {
            "buildkit": true
        },
        "registry-mirrors": [
            "https://5zpts8zx.mirror.aliyuncs.com"
        ]
    }

- 宝塔配置网站域名失败或者一直加载中

可能是由于你的项目文件太大、文件太多的原因
可以创建一个空文件夹，然后再设置域名到这个目录下
再修改配置文件

### 其他

由次项目，你可以自定义添加一些其他的服务，如 `elk`, 等等