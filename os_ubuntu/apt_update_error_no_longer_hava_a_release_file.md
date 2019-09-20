# apt update 报错：不存在Release文件

在使用Ubuntu 18.04上执行`apt update`更新包的时候，提示如下错误：
> E: The repository 'http://mirrors.ustc.edu.cn/ubuntu bionic Release' no longer has a Release file.
> N: Updating from such a repository can't be done securely, and is therefore disabled by default.
> N: See apt-secure(8) manpage for repository creation and user configuration details.

更换了几个源地址都报这个错误，而且登录源地址网站时存在Release文件的。

后经测试，发现在/etc/apt/source.list中应该使用https，而非http。
通过Ubuntu自带的源配置工具“Softwares&Update”配置后的source.list文件中也是http协议的地址，因此只能通过手工修改成https。

# apt update
apt update 从 /etc/apt/sources.list 和 /etc/apt/sources.list.d/xxxx.list 来寻找源下载包信息。
source.list中的示例如下：
> deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted

## 软件包的分类（Archive Type）
源地址格式的第一部分是软件包的分类，分为deb和deb-src。
1. deb表示二进制内容，会使用仓库中的二进制预编译软件包，可以直接通过 apt 来安装。
2. deb-src 表示源代码，在使用 apt 时会根据源代码来进行安装，通常可以使用 apt source $pacakge 来下载然后编译。

## 仓库地址 (Repository URL)
源地址格式的第二部分是仓库的地址。
在新版本中，需要使用https协议，否则会提示无法找到Release文件。

## 发型版本 (Distribution)
源地址格式的第三部分是Ubuntu的发行版本。
Ubuntu 1804 --> bionic
Ubuntu 1604 --> xenial

发行版还区分了更新为何种更新，例如：
bionic：版本更新
bionic-updates： 主要缺陷修复更新
bionic-backports：未经过官方严格测试的更新
bionic-security

## 组件（Component）
源地址格式中发行版之后的就是组件了，组件可以有多个。
### Debian
1. main 包含符合 DFSG 指导原则的自由软件包，而且这些软件包不依赖不符合该指导原则的软件包。这些软件包被视为 Debian 发型版的一部分
2. contrib 包含符合 DFSG 指导原则的自由软件包，不过这些软件包依赖不在 main 分类中的软件包
3. non-free 包含不符合 DFSG 指导原则的非自由软件包
### Ubuntu
1. main 官方支持的自由软件
2. restricted 官方支持的非完全自由的软件
3. universe 社区维护的自由软件
4. multiverse 非自由软件

## 输出标识
在运行 apt update 时输出的标识含义如下：
1. GET 表示在该源中有更新，并且新的内容已经被保存
2. HIT 表示已经在该源中有最新的包
3. IGN 表示包被忽略，要不然是没有更新，要不然就是该包已经被废弃，如果开发者改变了版本或者更换了仓库密钥也会这样


# 参考：
1. https://wiki.debian.org/SourcesList
2. https://einverne.github.io/post/2019/08/apt-update-get-hit-ign.html
