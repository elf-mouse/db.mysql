* 若本身存在默认值，则先删除

```
ALTER TABLE 表名 ALTER COLUMN 字段名 DROP DEFAULT;
```

* 若本身不存在，则可以直接设定

```
ALTER TABLE 表名 ALTER COLUMN 字段名 SET DEFAULT 默认值;
```
