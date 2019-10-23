# Docker 的使用

为了避免每次使用Docker命令时sudo，可将当前用户添加到docker用户组。
`sudo usermod -aG docker <username>`

## 1.Docker的核心概念：镜像、容器、仓库
镜像是静态文件，容器可以理解为是镜像的运行实例，仓库是存放镜像的地方。
在Docker里，存放一类镜像的则为仓库，例如存放Ubuntu各个镜像的是Ubuntu仓库。存放仓库的地方是仓库注册服务器。

## 2.镜像相关命令
### 获取镜像 (pull)
通过pull命令获取镜像：
`docker [image] pull [REGISTRY_SERVER]IMAGE_NAME[:TAG]`
如果没有指定TAG，则默认为latest。镜像的lastest标签意味着镜像的内容会跟踪最新版本的变更而变更，内容不稳定。因此，从稳定性考虑，不建议使用lastest标签。

示例：
`docker pull ubuntu:18.04`

### 列出本地镜像 (images/image ls)
通过以下命令查看本地所有镜像：
`docker images`
`docker image ls`
images 命令常用参数如下：
1. -a, --all=true|false: 列出所有镜像文件，包括临时文件，默认为否。
2. -f, --filter=[]: 过滤列出的镜像。

### 添加镜像标签 (tag)
使用tag命令为已有镜像添加标签。
示例：
`docker tag python:3 mypython:1.0.1`

### 查看镜像信息 (inspect)
使用inspect命令查看镜像的详细信息，包括制作者，适应架构、环境变量、数据卷、CMD命令等。
`docker [image] inspect IMAGE_NAME:TAG`

### 查看镜像历史 (history)
镜像文件是由多个层组成的，可以通过history命令查看各个层的具体内容。
`docker history --no-trunc IMAGE_NAME:TAG`
--no-trunc参数用于输出完整内容。

### 查找远程镜像 (search)
使用search命令来搜索仓库中的镜像：
`docker search [option] keyword`
常用的选项包括：
1. -f, --filter filter: 过滤输出内容。
2. --format string: 格式化输出内容。
3. --limit int: 限制输出结果个数，默认25个。
4. --no-trunc: 不截断输出结果。

### 删除本地镜像 (rmi/image rm)
可以通过标签或IMAGEID，删除单个镜像：
`docker rmi [IMAGE_NAME:TAG][IMAGEID]`
`docker image rm [IMAGE_NAME:TAG][IMAGEID]`
常用选项包括：
1. -f, --force: 强制删除镜像，即使有容器依赖他。
2. -no-prune: 不要清理未带标签的父镜像。

> 1.如果使用标签删除镜像时，当一个镜像包含多个标签的时候，docker rmi 命令只是删除了该镜像多个标签中的指定标签而已，并不影响镜像文件。但当镜像只剩下一个标签时，会删除镜像文件。
> 2.如果使用imageid删除镜像时，会先尝试删除所有指向该镜像的标签，然后删除镜像文件本身。

删除所有镜像：
`docker rmi $(docker images -q)`

### 清理无用镜像 (prune)
prune命令用来清理一些遗留的临时镜像文件和没有被使用的镜像。
`docker image prune`
常用的选项有：
1. -a, --all: 删除所有无用镜像，不光时临时镜像。
2. -filter filter：只清理符合给定过滤器的镜像。
3. -f, --force: 强制删除镜像。

### 创建镜像的3种方式
创建镜像有3种方式：
1. 基于已有容器：
`docker [container] commit [OPTIONS] CONTAINER[REPOSITORY[:TAG]]`
此种方式，需要先启动一个容器，在容器种做完修改后，执行commit命令创建镜像。

2. 导入镜像：
`docker [container] import`

3. 基于Dockerfile创建
`docker [image] build`

### 存出和加载镜像 (save, load)
如果要导出镜像文件到本地，可以使用
`docker [image] save -o <filepath>`

如果要把本地文件存入镜像库，可以使用
`docker [image] load -i <filepath>`

### 上传镜像 (push)
如果要删除镜像到仓库，可以通过push命令完成：
`docker [image] push IMAGE_NAME[:TAG]|[REGISTRY_HOST[:RESIGTRY_PORT]/]IMAGE_NAME[:TAG]`

## 3.容器
### 创建容器 (create)
使用create命令创建容器，新建的容器处于停止状态：
`docker [container] create`
创建容器时有很多选项，包括容器运行模式、容器环境配置、资源限制、安全保护等。
列举个别选项：
1. -i, --interactive=true|false: 保持标准输入打开，默认为false。
2. -t, --tty=true|false: 是否分配一个伪终端，默认为false。
3. -v, --volume: 挂载主机文件到容器内
4. --volume-driver="": 挂载文件卷的驱动类型
5. --volume-from=[] : 从其他容器挂载卷
6. -w, --workdir="" : 容器内的默认工作目录
7. -p, --publish=[] : 指定如何映射本地主机端口
8. --group-add=[] : 运行容器的用户组。
9. -e, --env=[] : 指定容器内的环境变量
10. -h, --hostname="" : 指定容器内的主机名
11. --name="" : 指定容器的别名
12. -m, --memory="" : 限制容器内应用的内容，单位可以是b,k,m或g

### 运行容器 (start)
通过docker create命令创建的容器处于停止状态，可以使用以下命令运行容器。
`docker [container] start <CONTAINER_NAME>`

### 查看容器 (ps/container ls)
如果要查看运行中的容器，可通过以下命令：
`docker ps`
`docker container ls`

如果要查看全部容器，可通过以下命令：
`docker ps -a`


### 创建并启动容器 (run)
`docker run`
如果要让容器守护态运行，需加上 -d 参数。
1. -i：保持标准输入打卡
2. -t: 打开一个伪终端
3. -d: 在后台运行容器

当使用exit退出bash进程时，容器也会自动退出。

### 查看容器输出
`docker [container] logs`

### 暂停容器 (pause, unpause)
使用pause命令暂停容器：
`docker [container] pause <CONTAINER>`

使用unpause命令重启容器：
`docker [container] unpause <CONTAINER>`

### 终止容器 (stop)
使用stop命令终止容器：
`docker [container] stop [-t|--time[=10]][CONATINER...]`
批量停止全部容器：
`docker container stop $(docker ps -a -q)`

还可以使用kill命令发送SIGKILL信号来强行停止容器：
`docker [container] kill <CONTAINER>`

### 重启容器 (restart)

### 进入容器 (attach, exec)

### 删除容器 (rm, prune, kill)
删除单个容器：
`docker container rm <CONTAINER>`
删除所有容器：
`docker container rm $(docker ps -a -q)`

如果要删除所有停止状态的容器，可执行：
`docker container prune`

### 查看容器 (inspect, top, stat)
