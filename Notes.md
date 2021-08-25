# CouchDB.Notes

组件名称：couchdb 
安装文档：https://docs.couchdb.org/en/latest/install/index.html#
配置文档：https://docs.couchdb.org/en/latest/config/index.html
支持平台：Debian家族 | RHEL家族 | Windows | macOS | Docker

责任人：helin

## 概要

**CouchDB** 是一个开源的面向文档的数据库管理系统，可以通过 RESTful JavaScript Object Notation (JSON) API 访问。CouchDb是一个存储Json文档的数据库。CouchDB是一个完全包含Web的数据库。使用JSON文档存储数据。使用Web浏览器通过HTTP访问您的文档。使用JavaScript 查询，组合和 转换文档。CouchDB适用于现代网络和移动应用程序。您可以使用CouchDB的增量复制高效地分发数据。

## 环境要求

* 程序语言：   erlang
* 应用服务器：
* 数据库:   
* 依赖组件：
* 其他：

## 安装说明

下面基于不同的安装平台，分别进行安装说明。

### 依赖

* Erlang OTP (19.x, 20.x >= 21.3.8.5, 21.x >= 21.2.3, 22.x >= 22.0.5)
* ICU  操作系统默认已安装
* OpenSSL common已安装
* Mozilla SpiderMonkey (1.8.5) 需yum/apt安装
* GNU Make 
* GNU Compiler Collection
* libcurl
* help2man
* Python (>=2.7) for docs
* Python Sphinx (>=1.1.3)

### CentOS

```shell
sudo yum -y install epel-release     #安装epel
vi /etc/yum.repos.d/bintray-apache-couchdb-rpm.repo

[bintray--apache-couchdb-rpm]
name=bintray--apache-couchdb-rpm
baseurl=http://apache.bintray.com/couchdb-rpm/el7/$basearch/
gpgcheck=0
repo_gpgcheck=0
enabled=1


sudo yum -y install couchdb #安装couchdb
sudo systemctl start couchdb
sudo systemctl enable couchdb

```

### Ubuntu

```shell
# 添加签名证书
sudo apt update && sudo apt install -y curl apt-transport-https gnupg
curl https://couchdb.apache.org/repo/keys.asc | gpg --dearmor | sudo tee /usr/share/keyrings/couchdb-archive-keyring.gpg >/dev/null 2>&1
source /etc/os-release
echo "deb [signed-by=/usr/share/keyrings/couchdb-archive-keyring.gpg] https://apache.jfrog.io/artifactory/couchdb-deb/ ${VERSION_CODENAME} main" | sudo tee /etc/apt/sources.list.d/couchdb.list >/dev/null

# 通过设置 debcouf-set-selection来绕过安装CouchDB过程中出现的交互，
# 同时设置DEBIAN_FRONTEND=noninteractive选项来避免交互
echo "couchdb couchdb/mode select none" | debconf-set-selections
apt update
DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes couchdb

# 由于绕过了交互，所以会出现couchdb正常启动。
# 会导致后面的systemctl restart couchdb命令失败，所以将/opt/couchdb/etc/local.ini配置文件中的最后一行关于设置admin用户的行的注释去掉
sed -i '95s/;//g' /opt/couchdb/etc/local.ini
```



## 路径

* 程序路径：     /opt/couchdb
* 日志路径：   /var/log/couchdb 
* 配置文件路径：/opt/couchdb/etc
* 启动路径:       /opt/couchdb/bin/couchdb
* 其他...

## 配置

安装完成后，需要依次完成如下配置

centos上

```shell
vi  /opt/couchdb/etc/default.ini
#bind_address=0.0.0.0


[admins]
#admin = mysecretpassword
```

## 账号密码

### 数据库密码

如果有数据库

* 数据库安装方式：
* 账号密码：

### 后台账号

如果有后台账号

* 登录地址  http://服务器IP:5984/_utils/

* 账号密码: 账户为 admin 密码为 mysecretpassword

* 密码修改方案：vi  /opt/couchdb/etc/local.ini   

  修改  admin=新密码


## 服务

本项目安装后有服务,可设置为开机自启

```
sudo systemctl enable couchdb                      
```

## 环境变量

列出需要增加的环境变量以及增加环境变量的命令：

* 名称 | 路径

## 版本号

通过如下的命令获取主要组件的版本号: 

```
# Check couchdb version
cd  /opt/couchdb/bin/
./couchdb -version
```

## 常见问题

#### 有没有管理控制台？

*http:// 公网 IP:5984

#### 本项目需要开启哪些端口？

| item | port |
| ---- | ---- |
| tcp  | 5984 |
| tcp  | 4369 |
| tcp  | 1024 |

#### 有没有CLI工具？

cdbcli

## 日志

* 2020-05-13 完成CentOS安装研究
