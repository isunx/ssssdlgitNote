预编译通过安全的数据绑定从根本上杜绝了SQL注入发生的可能，但是由于人为等原因，依旧存在可以被绕过的可能，感觉像oauth2.0本身是安全的，但是依旧有各种问题使其变得不安全。

预编译的原理：
就是语法树已经生成好了，传入的参数不管怎样也改变不了sql语句的语法结构，只会被当作参数处理。
> 	预编译使用占位符?代替字段值的部分，将SQL语句先交由数据库预处理，构建语法树，再传入真正的字段值多次执行，省却了重复解析和优化相同语法树的时间，提升了SQL执行的效率。  
	正因为在传入字段值之前，语法树已经构建完成，因此无论传入任何字段值，都无法再更改语法树的结构。至此，任何传入的值都只会被当做值来看待，不会再出现非预期的查询，这便是预编译能够防止SQL注入的根本原因。

- 可能开发人员没有正确的使用预编译语句，处于各种原因，还存在sql语句拼接参数的情况。
- 不是所有的参数都可以预编译，表名和列名出于生成语法树原理的问题，不能预编译，因为预编译要判断表明列明是否存在。这种情况依旧需要字符串拼接，然后order by后的ASC和DESC也是不能被编译的，也是需要字符串拼接，如果从前台传入，依旧可能存在问题。


- [SQL注入攻击防御之预编译的探究](https://cloud.tencent.com/developer/news/378220) 写的真的很好预编译的原理一下就清晰了
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
仔细像一下，技术摸底的时候感觉还是太紧张了，这个预编译早就看过了。但是问sql注入的时候愣是没说上来。

