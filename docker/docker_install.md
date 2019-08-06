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
`sudo add-apt-repository \`
	`"deb [arch=amd64] https://download.docker.com/linux/ubuntu \`
	`$(lsb_release -cs) \`
	`stable"`

命令`lsb_release -cs`用于获取系统代号，Ubuntu 18.04的代号为bionic。

## 安装Docker
`sudo apt-get update`
`sudo apt-get install docker-ce docker-ce-cli containerd.io`
安装成功后，会启动Docker服务。

## 测试Docker
`sudo docker run hello-world`
