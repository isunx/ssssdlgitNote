# 关于jinja2
jinja2是一个类似php smart引擎的视图模板，可以将内容动态的插入到html中去详细可以看一下[Jinja2 模板的学习](https://www.jianshu.com/p/8fc66b083ecd)

# 关于jinja2模板注入
这是一种代码注入，常见的测试手法是在可以回显的地方插入`{{2+2}}`如果返回了4就说明可能存在jinja模板注入  
