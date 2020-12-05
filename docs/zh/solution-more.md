# 更多...

下面每一个方案，都经过实践证明行之有效，希望能够对你有帮助

## 配置

参考官方方案：https://docs.couchdb.org/en/latest/config/index.html

## 域名绑定

当服务器上只有一个网站时，不做域名绑定也可以访问网站。但从安全和维护考量，**域名绑定**不可省却。

以示例网站为例，域名绑定操作步骤如下：

1. 确保域名解析已经生效  
2. 使用 SFTP 工具登录云服务器
3. 修改 [Nginx虚拟机主机配置文件](/zh/stack-components.md#nginx)，将其中的 **server_name** 项的值修改为你的域名
   ```text
   server
   {
   listen 80;
   server_name www.example.com;  # 此处修改为你的域名
   index index.html index.htm index.php;
   root  /data/wwwroot/www.example.com;
   ...
   }
   ```
4. 保存配置文件，重启 [Nginx 服务](/zh/admin-services.md#nginx)


## 开启远程访问

1. 修改 CouchDB 配置文件 */opt/couchdb/etc/default.ini*
   ```
  将 bindIP 修改为 0.0.0.0 或 本地电脑公网IP
      #bind_address = 127.0.0.1
      bind_address = 0.0.0.0
   ```
   > 0.0.0.0 代表任意公网IP均可访问

2. CouchDB
   ```
   systemctl restart couchdb
   ```

## 密码管理

### 重置密码

重置密码即已经忘记密码的情况下，通过特殊手段重新设置新密码的过程。

1. 修改 CouchDB 配置文件 */opt/couchdb/etc/local.ini*，将下面的$new_password替换成新密码
   ```
   admin = $new_password
   ```
2. 重启 CouchDB 服务
   ```
   systemctl restart couchdb
   ```

## 开启用户认证

1. 修改 CouchDB 配置文件 */opt/couchdb/etc/default.ini*
   ```
  将 require_valid_user 的值设置为 false， 则每个人都必须经过身份验证。
   [chttpd]
   require_valid_user = false
   ```

2. CouchDB
   ```
   systemctl restart couchdb
