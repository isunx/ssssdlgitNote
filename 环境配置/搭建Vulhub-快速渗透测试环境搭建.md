[项目地址](https://github.com/vulhub/vulhub)
[官网](https://vulhub.org/)

# 安装

```
# 安装docker，直接在官网上安装最新版的docker，也可以使用系统自带的包管理工具安装（yum、apt、rpm）
curl -s https://get.docker.com/ | sh 
# 安装pip 应该是也要先准备好python
curl -s https://bootstrap.pypa.io/get-pip.py | python
# 安装docker-compose
pip install docker-compose
# 这里可能会提示requests版本问题，直接忽略就好了，然后安装好启动的时候，有可能会遇到gssapi中没有一个什么方法直接安装以下组件就可以了
yum install python-paramiko -y
# 安装完成后查看版本,没有报错说明安装docker-compose成功
docker-compose -v
# 找到一个合适的目录，下载Vulhub,这里面包含了很多测试环境的配置文件
git clone https://github.com/vulhub/vulhub.git
```

# 搭建简单测试环境

# 未完这个下载不知道为啥一直就卡在那里不动了，有一个一直是writing的状态
记录一下关于使用daocloud
- 注册DaoCloud
- 执行docker login daocloud.io
- 输入daocloud用户名密码，显示登录成功
- 在daocloud网页上查询镜像，选择之后，点击”拉取”
- 在弹出的窗口里复制拉取镜像字符串

6)     在你的主机上继续执行#docker pull daocloud.io/library/python:2.7.7
