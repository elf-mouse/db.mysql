**错误描述：**

添加用户 `insert into mysql.user(Host,User,Password) values("localhost","test",password("1234"));`

报以下的错误 `ERROR 1364 (HY000): Field 'ssl_cipher' doesn't have a default value`错误

mysql5.1 以上版本，我是在 5.6 版本上操作的。

**错语原因：**

mysql 用户表的中某些字段不能为空，没有默认值，其实是操作错误，mysql 添加用户是不能这样直接 insert user 表的。

**解决方法：**

正确的添加用户方法：

`GRANT USAGE ON *.* TO 'test'@'localhost' IDENTIFIED BY '123456' WITH GRANT OPTION;`

用户：test，密码：123456，这样就添加了一个新的用户，不会出以上的错误了。

---

**Error Code: 1175.**

> You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column To disable safe mode, toggle the option in Preferences -> SQL Queries and reconnect.

解决办法是在当前 session 下执行如下的语句

`SET SQL_SAFE_UPDATES = 0;`

---

Q: `SQLSTATE[HY000]: General error: 1030 Got error 28 from storage engine`

A: Mysql error "28 from storage engine" - means "not enough disk space".

```
# To show disc space use command below.
df -h
```

> clear log files

---

Q: `MySQL error 1449: The user specified as a definer does not exist`

A: `mysql_upgrade -u root`
