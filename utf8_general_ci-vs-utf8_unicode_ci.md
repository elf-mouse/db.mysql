## 简短总结

* `utf8_unicode_ci`和`utf8_general_ci`对中、英文来说没有实质的差别。
* `utf8_general_ci`校对速度快，但准确度稍差。
* `utf8_unicode_ci`准确度高，但校对速度稍慢。

如果你的应用有德语、法语或者俄语，请一定使用`utf8_unicode_ci`；一般用`utf8_general_ci`就够了。

## 详细总结

1. 对于一种语言仅当使用`utf8_unicode_ci`排序做的不好时，才执行与具体语言相关的utf8字符集校对规则。例如，对于德语和法语，`utf8_unicode_ci`工作的很好，因此不再需要为这两种语言创建特殊的utf8校对规则。
2. `utf8_general_ci`也适用与德语和法语，除了'?'等于's'，而不是'ss'之外。如果你的应用能够接受这些，那么应该使用 `utf8_general_ci`，因为它速度快。否则，使用`utf8_unicode_ci`，因为它比较准确。

用一句话概况上面这段话：`utf8_unicode_ci`比较准确，`utf8_general_ci`速度比较快。通常情况下 `utf8_general_ci`的准确性就够我们用的了，在我看过很多程序源码后，发现它们大多数也用的是`utf8_general_ci`，所以新建数据 库时一般选用`utf8_general_ci`就可以了

## 如何在MySQL中使用UTF8

在 _my.cnf_ 中增加下列参数

```
[mysqld]
init_connect='SET NAMES utf8′
default-character-set=utf8
default-collation = utf8_general_ci
```

执行查询 `mysql> show variables;` 相关如下: 

```
character_set_client | utf8 
character_set_connection | utf8 
character_set_database | utf8 
character_set_results | utf8 
character_set_server | utf8 
character_set_system | utf8
collation_connection | utf8_general_ci 
collation_database | utf8_general_ci 
collation_server | utf8_general_ci
```
