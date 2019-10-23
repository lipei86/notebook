# Docker的安装

## 安装包以允许apt使用远程仓库
`sudo apt-get install apt-transport-https`
`sudo apt-get install ca-certificates`
`sudo apt-get install curl`
`sudo apt-get install gnupg-agent`
`sudo apt-get install software-properties-common`

## 添加Docker官方GPG密钥
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`
通过以下命令确认导入指纹为“9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88”的公钥：
`sudo apt-key fingerprint 0EBFCD88`

## 添加源
`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

命令`lsb_release -cs`用于获取系统代号，Ubuntu 18.04的代号为bionic。

## 安装Docker
`sudo apt-get update`
`sudo apt-get install docker-ce docker-ce-cli containerd.io`
安装成功后，会启动Docker服务。

## 使用镜像加速器
### 获取加速器地址
进入阿里云的“容器镜像服务”，点击“镜像加速器”，即可看到供本人使用的加速器地址。
### 配置加速器
`sudo mkdir -p /etc/docker`
`sudo tee /etc/docker/daemon.json <<-'EOF'`
`{`
  `"registry-mirrors": [
		"https://34eryx3n.mirror.aliyuncs.com"
		, "https://docker.mirrors.ustc.edu.cn"
		, "https://dockerhub.azk8s.cn"
		, "https://reg-mirror.qiniu.com"]`
`}`
`EOF`
`sudo systemctl daemon-reload`
`sudo systemctl restart docker`

可以通过`docker info`命令来查看镜像是否启用
## 测试Docker
`sudo docker run hello-world`
Docker在本地未找到hello-world镜像，会从远程下载镜像。
