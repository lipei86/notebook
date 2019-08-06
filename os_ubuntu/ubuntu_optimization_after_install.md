# Ubuntu 安装后的优化

> 环境：Ubuntu 18.04

## 更改源为阿里云源

### 方法一：更改sources.list文件
拷贝附件中sources.list到服务器中，替换/etc/apt/sources.list文件

### 方法二：更改Software & Updates配置
进入“Software & Updates”，更改DownloadFrom选项为mirrors.aliyun.com

### 更改完成后更新
`sudo apt-get update`


## 安装中文语言包
`sudo apt-get install language-pack-zh-hans`

## 安装搜狗输入法
`echo deb http://archive.ubuntukylin.com:10006/ubuntukylin trusty main | sudo tee /etc/apt/sources.list.d/ubuntukylin.list`
`sudo apt-get update`
`sudo apt-get install sogoupinyin`
安装完成后重启系统即可

> 搜狗输入使用Fcitx，如果重启后切换不出搜狗输入法，可进入“Fcitx Configuration”，在"Input Method"列表中，添加上"Sougou Pinyin"即可。

> Fcitx的安装目录在/usr/share/fcitx。

## 安装WPS
`sudo apt-get install wps-office`

## 移除LibreOffice
`sudo apt-get remove libreoffice`

## 安装Git
`sudo apt-get install git`

## 安装Docker
`sudo apt-get install docker-ce`
