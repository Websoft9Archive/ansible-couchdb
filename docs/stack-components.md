# Parameters

The CouchDB deployment package contains a sequence software (referred to as "components") required for CouchDB to run. The important information such as the component name, installation directory path, configuration file path, port, version, etc. are listed below.

## Path

### CouchDB

CouchDB installation directory:  */data/couchdb*  
CouchDB logs directory:  */data/logs/couchdb*   

### Nginx

Nginx vhost configuration file: */etc/nginx/sites-available/default.conf*  
Nginx main configuration file: */etc/nginx/nginx.conf*  
Nginx logs file: */var/log/nginx/*

## Ports

You can control(open or shut down) ports by **[Security Group Setting](https://support.websoft9.com/docs/faq/zh/tech-instance.html)** of your Cloud Server whether the port can be accessed from Internet.

You can run the cmd `netstat -tunlp` to list all used ports, and we list the following most useful ports for you:

| Name | Number | Use |  Necessity |
| --- | --- | --- | --- |
| HTTP | 5984 | HTTP requests for CouchDB Console| Optional |
| HTTP | 80 |  nginx HTTP port | Required |
| HTTP | 443 | nginx HTTPS port| Optional |


## Version

You can see the version from product page of Marketplace. However, after being deployed to your server, the components will be automatically updated, resulting in a certain change in the version number. Therefore, the exact version number should be viewed by running the command on the server:

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
