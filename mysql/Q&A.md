__错误描述：__

添加用户 `insert into mysql.user(Host,User,Password) values("localhost","test",password("1234"));`

报以下的错误 `ERROR 1364 (HY000): Field 'ssl_cipher' doesn't have a default value`错误

mysql5.1以上版本，我是在5.6版本上操作的。

__错语原因：__

mysql用户表的中某些字段不能为空，没有默认值，其实是操作错误，mysql添加用户是不能这样直接insert user表的。

__解决方法：__

正确的添加用户方法：

`GRANT USAGE ON *.* TO 'test'@'localhost' IDENTIFIED BY '123456' WITH GRANT OPTION;`

用户：test，密码：123456，这样就添加了一个新的用户，不会出以上的错误了。

__Error Code: 1175.__

> You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Queries and reconnect.

解决办法是在当前session下执行如下的语句

`SET SQL_SAFE_UPDATES = 0;`
