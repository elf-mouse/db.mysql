## 1. 导出整个数据库

`mysqldump -u USERNAME -p DATABASENAME > /path/to/EXPORT_FILENAME`

## 2. 导出一个表

`mysqldump -u USERNAME -p DATABASENAME TABLENAME > /path/to/EXPORT_FILENAME`

## 3. 导出一个数据库结构

`mysqldump -u USERNAME -p -d --add-drop-table DATABASENAME > /path/to/EXPORT_FILENAME`

> `-d` 没有数据 `--add-drop-table` 在每个create语句之前增加一个drop table

## 4. 导入数据库（登录mysql）

```
mysql> use DATABASENAME;
mysql> source /path/to/IMPORT_FILENAME;
```
