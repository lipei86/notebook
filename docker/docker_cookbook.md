# Docker 的使用

## 添加用户到docker用户组
为了避免每次使用Docker命令时sudo，可将当前用户添加到docker用户组。
`sudo usermod -aG docker <username>`

# Docker的核心概念：镜像、容器、仓库
镜像是静态文件，容器可以理解为是镜像的运行实例，仓库是存放镜像的地方。
在Docker里，存放一类镜像的则为仓库，例如存放Ubuntu各个镜像的是Ubuntu仓库。存放仓库的地方是仓库注册服务器。

# 镜像
## 通过以下命令获取镜像
`docker [image] pull [REGISTRY_SERVER]NAME[:TAG]`
不指定TAG，默认为latest
例如
`docker pull ubuntu:18.04`

## 列出本地镜像
`docker images`
或
`docker image ls`

## 使用tag命令添加新的镜像标签
`docker tag python:3 mypython:1.0.1`

## 使用inspect命令查看详细信息
`docker [image] inspect NAME:TAG`

## 查找远程镜像
`docker search [option]`

## 删除本地镜像
`docker rmi [NAME:TAG][IMAGEID]`
或
`docker image rm [NAME:TAG][IMAGEID]`

## 清理无用镜像
`docker image prune`

## 创建镜像
创建镜像有3种方式：
1. 基于已有容器：
`docker [container] commit`
2. 导入镜像：
`docker [container] import`
3. 基于Dockerfile创建
`docker [image] build`

## 存出和加载镜像
如果要导出镜像文件到本地，可以使用
`docker [image] save`
如果要把本地文件存入镜像库，可以使用
`docker [image] load`

## 上传镜像
`docker [image] push NAME[:TAG]|[REGISTRY_HOST[:RESIGTRY_PORT]/]NAME[:TAG]`
默认上传到Docker Hub.


# 容器
## 创建容器
`docker [container] create`

## 运行容器
通过docker create命令创建的容器处于停止状态，可以使用以下命令运行容器。
`docker [container] start`

## 查看容器
`docker ps` 查看的是运行中的容器
`docker ps -a` 查看的是全部容器
`docker container ls`

## 创建并启动
`docker run`
当使用exit退出bash进程时，容器也会自动退出。
如果要让容器守护态运行，需加上 -d 参数。
-i：保持标准输入打卡
-t: 打开一个伪终端
-d: 在后台运行容器

## 查看容器输出
`docker [container] logs`

## 暂停容器
`docker [container] pause`
可以使用以下命令重启：
`docker [container] unpause`

## 终止容器
`docker [container] stop`
