# 百度杯十月场 Gift
打开题目，post发get包,得到报错`More information is available with DEBUG=True.`，发现是django
```
POST / HTTP/1.1
Host: c0a0e53c0f2d4f4fa60e8850469e05c794f99e0dbd734ea1.changame.ichunqiu.com
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Upgrade-Insecure-Requests: 1

```

github上找到压缩文件，破解密码解压发现是django的secret key

```
# 根据提示生成生日字典
python pydictor.py -plug birthday 19900101 20141231 --len 8 8
# 使用字典爆破压缩包，密码是20001111
fcrackzip -D -p /usr/share/wordlists/rockyou.txt -u crack_this.zip
```

找到django命令执行poc
```

```