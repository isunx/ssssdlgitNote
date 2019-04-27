# 环境搭建
- Windows 10
- python3
- flask
- jinja2

# 测试代码
```
from flask import Flask, render_template, render_template_string

app = Flask(__name__)  
 
@app.route("/user/<name>")
def user(name):
    template = '''
    <h3>%s</h3>
    '''%(name)
    return render_template_string(template)

if __name__ == "__main__":  
    app.run() 

```
就是把url user后面的name输出出来
> 注意这里面如果使用render_template带入html模板的话就不会产生这个问题

