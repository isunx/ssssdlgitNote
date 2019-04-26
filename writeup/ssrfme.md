---
题目地址：（HITCON2017）题目并不是你想要的http://117.50.3.97:8004
---
 
直接点开源码，读一下
```
<?php 
    $sandbox = "sandbox/" . md5("orange" . $_SERVER["REMOTE_ADDR"]);   //定义一个路径
    @mkdir($sandbox);  //创建路径
    @chdir($sandbox);  //切换到这个路径

    $data = shell_exec("GET " . escapeshellarg($_GET["url"]));  // escapeshellarg是将字符转码成可以再命令行里面执行的
    $info = pathinfo($_GET["filename"]); //返回路径中有关信息会返回一个数组，里面有文件名，路径，文件后缀等等信息，比如/etc/httpd/conf/httpd.conf 返回的dirname里面就是/etc/httpd/conf
    $dir  = str_replace(".", "", basename($info["dirname"]));   //basename返回路径中文件名的部分 接着上面的例子  basename($info["dirname"])的结果就是conf
    @mkdir($dir); //创建路径
    @chdir($dir); //切换到路径
    @file_put_contents(basename($info["basename"]), $data); //将data写到basename($info["basename"])文件里面
    highlight_file(__FILE__); 
```

解题思路：
 $data = shell_exec("GET " . escapeshellarg($_GET["url"]));  这里面可定存在命令执行

