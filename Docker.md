# Docker 基本使用方法

## 1. 环境准备与基础命令

*   **安装 Docker:** (不同操作系统安装方式不同，请参考官方文档: [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/))
*   **启动 Docker 服务:** (通常在安装后会自动启动)
    ```bash
    sudo systemctl start docker  # Linux (systemd)
    ```

## 2. 镜像操作 (Images)

*   **拉取镜像:** 从 Docker Hub 或其他注册中心下载镜像。
    ```bash
    docker pull ubuntu:latest  # 拉取最新版本的 Ubuntu 镜像
    docker pull nginx:1.23.3 # 拉取指定版本 Nginx 镜像
    ```
*   **搜索镜像:** 在 Docker Hub 上搜索镜像。
    ```bash
    docker search nginx
    ```
*   **查看本地镜像列表:**
    ```bash
    docker images
    ```
*   **删除镜像:**  (需要先停止所有使用该镜像的容器)
    ```bash
    docker rmi <image_id>  # 通过 ID 删除
    docker rmi <image_name>:<tag> #通过名称和标签删除
    ```

## 3. 容器操作 (Containers)

*   **创建并运行容器:**
    ```bash
    docker run -d --name my-container ubuntu:latest  # 在后台运行一个名为 my-container 的 Ubuntu 容器
    docker run -it ubuntu:latest /bin/bash #交互式运行，进入容器的 bash shell
    ```

    *   `-d`:  在后台（detached）模式运行。
    *   `--name <container_name>`: 为容器指定一个名称。
    *   `-i`: 保持 STDIN 打开，即使没有连接。
    *   `-t`: 分配一个伪终端。
    *   `-it`:  组合 `-i` 和 `-t`，提供交互式终端。

*   **启动已停止的容器:**
    ```bash
    docker start <container_id> 或 docker start <container_name>
    ```
*   **停止运行中的容器:**
    ```bash
    docker stop <container_id> 或 docker stop <container_name>
    ```

*   **查看正在运行的容器:**
    ```bash
    docker ps
    ```
*   **查看所有容器 (包括已停止的):**
    ```bash
    docker ps -a
    ```
*   **删除容器:**  (需要先停止容器)
    ```bash
    docker rm <container_id> 或 docker rm <container_name>
    ```

## 4. Dockerfile 操作 (构建镜像)

*   **编写 Dockerfile:**  Dockerfile 是一个文本文件，包含用于创建 Docker 镜像的指令。
    ```dockerfile
    # 使用官方 Ubuntu 作为基础镜像
    FROM ubuntu:latest

    # 安装一些必要的包
    RUN apt-get update && apt-get install -y --no-install-recommends \
        nginx \
        curl

    # 复制本地文件到容器中
    COPY ./html /var/www/html

    # 暴露端口
    EXPOSE 80

    # 定义启动命令
    CMD ["nginx", "-g", "daemon off;"]
    ```

*   **构建镜像:**  使用 Dockerfile 构建镜像。
    ```bash
    docker build -t my-nginx:1.0 . # 从当前目录 ('.') 构建一个名为 my-nginx:1.0 的镜像
    ```
    * `-t`: 指定镜像名称和标签。

## 5. 网络操作

*   **查看容器的网络设置:**
    ```bash
    docker inspect <container_id>  # 查看详细信息，包括网络配置
    ```
*   **将容器端口映射到宿主机端口:** (在 `docker run` 命令中使用 `-p` 参数)
    ```bash
    docker run -d -p 8080:80 my-nginx:1.0  # 将容器的 80 端口映射到宿主机的 8080 端口
    ```

## 6. Docker Volume 操作 (数据持久化)

*   **创建 volume:**
    ```bash
    docker volume create myvolume
    ```
*   **运行容器并挂载 volume:**
    ```bash
    docker run -d -v myvolume:/var/www/html my-nginx:1.0 #将myvolume挂载到容器的/var/www/html目录
    ```

## 7. 其他常用命令

*   **查看 Docker 信息:**
    ```bash
    docker info
    ```
*   **清理无用的数据 (停止的容器、网络、镜像等):**
    ```bash
    docker system prune -a  # 清理所有无用数据，包括未使用的镜像和 volume
    ```

**重要提示：**

*   `docker run` 命令有很多选项，可以根据需要进行调整。
*   Docker Hub 是一个公共的 Docker 镜像仓库，你可以从中获取各种各样的镜像。
*   Dockerfile 的编写需要一定的学习成本，建议参考官方文档和示例。
*  在实际使用中，经常会结合多个命令来完成复杂的任务。

希望这份指南能帮助你入门 Docker！
