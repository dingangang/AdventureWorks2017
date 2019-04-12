# AdventureWorks2017
ubuntu sqlserver sampleData

## 下载文件 download

```
  wget https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak
```
或者你可以直接从我的库中下载。 OR

```
  wget https://github.com/dingangang/AdventureWorks2017/raw/master/AdventureWorks2017.bak
```

## 移动文件到mssql文件夹   move data to mssql dir

### 注意自己的路径   watch your path

```
  $ sudo mkdir -p /var/opt/mssql/backup
```

```
 $ sudo mv /home/%YOUR_USER_NAME%/AdventureWorks2017.bak /var/opt/mssql/backup/
```

## 进入到mssql   enter mssql

```
$ sqlcmd -S localhost -U SA
```

## 获取备份信息逻辑名称LogicalName    got the logicalName

```
1> RESTORE FILELISTONLY from DISK = '/var/opt/mssql/backup/AdventureWorks2017.bak'
2> GO
```

### 下面是示例返回     sample result

信息可能比较多，有用的只有LogicalName    only LogicalName is useful
```
LogicalName             
---------------------------------------------------------
AdventureWorks2017                                       
AdventureWorks2017_log                                                                                              

(2 rows affected)
```

现在我们获得逻辑名称  now we get the LogicalName

1、AdventureWorks2017

2、AdventureWorks2017_log

## 开始恢复数据库  try to restore

```
1> RESTORE DATABASE AdventureWorks
2> FROM DISK = '/var/opt/mssql/backup/AdventureWorks2017.bak'
3> WITH MOVE 'AdventureWorks2017' TO '/var/opt/mssql/data/AdventureWorks2017.mdf',
4> MOVE 'AdventureWorks2017_log' TO '/var/opt/mssql/data/AdventureWorks2017.ldf'
5> GO
```

刷新数据库。就可以看到了。 end.


