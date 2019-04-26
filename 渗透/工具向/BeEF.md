# BeEF相关配置（包含关联msf）
修改 /usr/share/beef-xss/config.yaml
```
metasploit:
	enable: ture
```
修改 /usr/share/beef-xss/extensions/demos/config.yaml
```
enable true
```
修改 /usr/share/beef-xss/extensions/metasploit/config.yaml
```
	ssl: true
	ssl_version: 'TLSv1'
```
修改默认管理员密码 /etc/beef-xss/config.yaml 默认beef beef,这个文件还可以改关于，端口js文件名等

# 启动beef+msf
启动相关服务
```
service postgresql start
service metasploit start
```
启动msf(注意这里的用户名密码和主机地址都添加beef的)
```
msfconsole
load msgrpc ServerHost=127.0.0.1 User=beef Pass=beef SSL=y
```
启动beef
```
/usr/share/beef-xss/beef
```
# 关于url
beef默认管理界面：http://127.0.0.1:3000/ui/panel
beef攻击js：http://127.0.0.1:3000/hook.js
beef demo测试界面：http://127.0.0.1:3000/hook.js

有点难用，顶不住了