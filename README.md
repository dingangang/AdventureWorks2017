# AdventureWorks2017
ubuntu sqlserver sampleData

## 下载文件

```
  wget https://github.com/dingangang/AdventureWorks2017/blob/master/AdventureWorks2017.bak
```

## 移动文件到mssql文件夹

### 注意自己的路径

```
  $ sudo mkdir -p /var/opt/mssql/backup
```

```
 $ sudo mv /home/user/AdventureWorks2017.bak /var/opt/mssql/backup/
```

## 进入到mssql

```
$ sqlcmd -S localhost -U SA
```

## 获取备份信息逻辑名称LogicalName

```
1> RESTORE FILELISTONLY from DISK = '/var/opt/mssql/backup/AdventureWorks2017.bak'
2> GO
```

### 下面是示例返回

信息可能比较多，有用的只有LogicalName
```
LogicalName             
---------------------------------------------------------
AdventureWorks2017                                       
AdventureWorks2017_log                                                                                              

(2 rows affected)
```

现在我们去到逻辑名称

1、AdventureWorks2017 
2、AdventureWorks2017_log

## 开始恢复数据库

```
1> RESTORE DATABASE AdventureWorks
2> FROM DISK = '/var/opt/mssql/backup/AdventureWorks2017.bak'
3> WITH MOVE 'AdventureWorks2017' TO '/var/opt/mssql/data/AdventureWorks2017.mdf',
4> MOVE 'AdventureWorks2017_log' TO '/var/opt/mssql/data/AdventureWorks2017.ldf'
5> GO
```

刷新数据库。就可以看到了。


