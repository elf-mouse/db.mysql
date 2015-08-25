## MySQL 中新建用户和用户权限

### 1. 创建新用户

```
// 登录MYSQL
mysql -u root -p
// 登录成功
// 创建用户
mysql> insert into mysql.user(Host,User,Password) values('localhost','test',password('test'));
// 刷新系统权限表
mysql> flush privileges;
// 这样就创建了一个名为：test 密码为：test的用户。

// 退出后登录一下
mysql> exit;

// 登录 test
mysql -u test -p
mysql> 登录成功
```

### 2. 为用户授权

```
// 登录MYSQL（有ROOT权限）
mysql -u root -p

// 首先为用户创建一个数据库（testDB）
mysql> create database testDB;
// 授权test用户拥有testDB数据库的所有权限
mysql> grant all privileges on testDB.* to test@localhost identified by 'test';
// 刷新系统权限表
mysql> flush privileges;
mysql> 其它操作
// 如果想指定部分权限给一用户，可以这样来写：
mysql> grant select,update on testDB.* to test@localhost identified by 'test';
// 刷新系统权限表。
mysql> flush privileges;
mysql> grant 权限1,权限2,…权限n on 数据库名称.表名称 to 用户名@用户地址 identified by '连接口令';
```

* 权限1,权限2,…权限n代表select,insert,update,delete,create,drop,index,alter,grant,references,reload,shutdown,process,file等14个权限。
* 当权限1,权限2,…权限n被all privileges或者all代替，表示赋予用户全部权限。
* 当数据库名称。表名称被.代替，表示赋予用户操作服务器上所有数据库所有表的权限。
* 用户地址可以是localhost，也可以是ip地址、机器名字、域名。也可以用’%’表示从任何地址连接。
* '连接口令'不能为空，否则创建失败。

例如：

```
mysql> grant select,insert,update,delete,create,drop on vtdc.employee to jee@10.163.225.87 identified by '123';
// 给来自10.163.225.87的用户jee分配可对数据库vtdc的employee表进行select,insert,update,delete,create,drop等操作的权限，并设定口令为123。

mysql> grant all privileges on vtdc.* to jee@10.10.10.87 identified by '123';
// 给来自10.163.225.87的用户jee分配可对数据库vtdc所有表进行所有操作的权限，并设定口令为123。

mysql> grant all privileges on . to jee@10.10.10.87 identified by '123';
// 给来自10.163.225.87的用户jee分配可对所有数据库的所有表进行所有操作的权限，并设定口令为123。

mysql> grant all privileges on . to jee@localhost identified by '123';
// 给本机用户jee分配可对所有数据库的所有表进行所有操作的权限，并设定口令为123。
```

### 3. 删除用户

```
@> mysql -u root -p
@> 密码
mysql> DELETE FROM user WHERE User=”jeecn” and Host=”localhost”；
mysql> flush privileges;
// 删除用户的数据库
mysql> drop database jeecnDB;
```

### 4. 修改指定用户密码

```
@> mysql -u root -p
@> 密码
mysql> update mysql.user set password=password('新密码') where User="jeecn" and Host="localhost";
mysql> flush privileges;
mysql> quit;
