# Docker Compose 的安装

## 下载指定版本的Docker Compose
sudo wget --continue --tries=0 --timeout=5 https://github.com/docker/compose/releases/download/1.25.0-rc2/docker-compose-`uname -s`-`uname -m` -O /usr/local/bin/docker-compose -o /usr/local/bin/wget-docker-compose.log
`sudo chmod +x /usr/local/bin/docker-compose`


具体Compose与Docker Engine的对应关系，可以参考https://github.com/docker/compose/releases。

## 参考
1. https://github.com/docker/compose/releases/tag/1.25.0-rc2
