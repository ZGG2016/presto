# oracle connector

版本：0.266

更多解释见官网：[https://prestodb.io/docs/0.266/connector/oracle.html](https://prestodb.io/docs/0.266/connector/oracle.html)

--------------------------------------

作用： 允许在外部 oracle 数据库中查询和创建表，这可以用来连接不同系统中的数据，比如 hive 和 oracle，或两个 oracle 实例。

使用：

1.添加 oracle.properties 文件

```sh
[root@bigdata101 etc]# cat catalog/oracle.properties 
connector.name=oracle
connection-url=jdbc:oracle:thin:[用户名]/[密码]@//[ip地址]:[端口]/[服务名]
```

这里使用官网提供的格式，执行如下查询时会报错 `Query 20220315_033219_00001_swu4z failed: ORA-01017: invalid username/password; logon denied`。

具体解释见：[https://www.cnblogs.com/wind-man/p/14167188.html](https://www.cnblogs.com/wind-man/p/14167188.html)

2.下载 `orai18n-12.1.0.2.0.jar` ，放到 `/opt/module/presto-0.266/plugin/oracle` 目录下。

下载地址：[https://mvnrepository.com/artifact/cn.easyproject/orai18n](https://mvnrepository.com/artifact/cn.easyproject/orai18n)

没有这个 jar 包会报错 `不支持的字符集 (在类路径中添加 orai18n.jar): ZHS16GBK`

3.重启 presto 后，指定 catalog 打开客户端

```sh
[root@bigdata101 presto-0.266]# ./prestocli --server 192.168.xx.xx:8080 --catalog oracle
presto> SHOW SCHEMAS FROM oracle;
....
```
