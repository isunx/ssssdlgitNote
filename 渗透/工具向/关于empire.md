---
以前就听说过这个工具，是一个后渗透神器
---
# 简单介绍一个生成木马建立监听的过程
首先安装,我在用的是2.5版本的，大概在2.0之后的版本和之前的命令就不太一样了，现在网上很多教程都是1.x的就导致我学习的时候走了很多弯路
```
# kali clone项目到本地
git clone https://github.com/EmpireProject/Empire.git
# 安装
sudo ./Empire/setup/indtall.sh
# 可能要输入一个什么密码，直接回车就可以，全部执行完成后就算完成了，需要的话还可以把./Empire/empire添加到系统命令中
```

简单使用，empire主要分为三个部分，
- module是一些payload，可以通过这个模块生成各种需要的后门之类的，对应的调用命令是usemobule和usestager