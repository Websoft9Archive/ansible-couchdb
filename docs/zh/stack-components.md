---
sidebarDepth: 3
---

# 参数

CouchDB 预装包包含 CouchDB 运行所需一序列支撑软件（简称为“组件”），下面列出主要组件名称、安装路径、配置文件地址、端口、版本等重要的信息。

## 路径

### CouchDB

CouchDB 安装目录： */data/couchdb*  
CouchDB 日志目录： */data/logs/couchdb*  

### Nginx

Nginx vhost 配置文件: */etc/nginx/sites-available/default.conf*  
Nginx main 配置文件: */etc/nginx/nginx.conf*  
Nginx 日志文件路径 : */var/log/nginx/*



## 端口号

在云服务器中，通过 **[安全组设置](https://support.websoft9.com/docs/faq/zh/tech-instance.html)** 来控制（开启或关闭）端口是否可以被外部访问。 

通过命令`netstat -tunlp` 看查看相关端口，下面列出可能要用到的端口：

| 名称 | 端口号 | 用途 |  必要性 |
| --- | --- | --- | --- |
| HTTP | 5984 | 通过 HTTP 访问 CouchDB 控制台 | 必选 |
| HTTP | 80 | 通过 nginx转发后HTTP 访问 | 可选 |
| HTTP | 443 | 通过HTTPs 访问 CouchDB 控制台 | 可选 |

## 版本号

组件版本号可以通过云市场商品页面查看。但部署到您的服务器之后，组件会自动进行更新导致版本号有一定的变化，故精准的版本号请通过在服务器上运行命令查看：

```shell
# Check all components version
sudo cat /data/logs/install_version.txt

# Linux Version
lsb_release -a

# Nginx Version
nginx -v

# CouchDB version
cat /data/wwwroot/couchdb/releases/*/couchdb.rel  |sed -n 3p | awk -F '"' '{print $4}'
```
