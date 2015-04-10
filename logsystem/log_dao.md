# Dao的日志初探

## 终于讲到Dao的日志了

```
2015-03-30 10:49:49,836 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:23) INFO  - Init file-pool by: C:\Users\wendal/.nutz/tmp/dao/ [200000]
2015-03-30 10:49:49,837 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:37) DEBUG - file-pool.home: 'C:\Users\wendal\.nutz\tmp\dao'
2015-03-30 10:49:49,843 org.nutz.filepool.NutFilePool.<init>(NutFilePool.java:66) INFO  - file-pool.cursor: 120
2015-03-30 10:49:49,848 org.nutz.dao.jdbc.Jdbcs.<clinit>(Jdbcs.java:85) DEBUG - Jdbcs init complete
2015-03-30 10:49:49,849 org.nutz.dao.jdbc.Jdbcs.getExpert(Jdbcs.java:98) INFO  - Get Connection from DataSource for JdbcExpert
2015-03-30 10:49:50,062 org.nutz.dao.impl.DaoSupport$1.invoke(DaoSupport.java:165) DEBUG - JDBC Driver --> mysql-connector-java-5.1.34 ( Revision: jess.balint@oracle.com-20141014163213-wqbwpf1ok2kvo1om )
2015-03-30 10:49:50,063 org.nutz.dao.impl.DaoSupport$1.invoke(DaoSupport.java:166) DEBUG - JDBC Name   --> MySQL Connector Java
2015-03-30 10:49:50,063 org.nutz.dao.impl.DaoSupport.setDataSource(DaoSupport.java:174) DEBUG - Database info --> MYSQL:[MySQL - 5.5.5-10.1.2-MariaDB]
2015-03-30 10:49:50,070 org.nutz.resource.Scans.scan(Scans.java:228) DEBUG - Found 4 resource by src( net/wendal/nutzbook/ ) , regex( ^.+[.]class$ )
2015-03-30 10:49:50,120 org.nutz.dao.impl.sql.run.NutDaoExecutor._runSelect(NutDaoExecutor.java:193) DEBUG - SELECT COUNT(*) FROM t_user 
```

## 还有什么同义词啊,啊啊啊, 逐行分析Log?

* 第一条, 初始化文件池,这是操作Blob/Clob时用到的东西,在虚拟主机使用nutz的时候有可能报错,这时候可以通过修改 *org/nutz/dao/jdbc/nutz_jdbc_experts.js* 修改里面的路径
* 第二条及第三条,提示路径及当前的偏移量
* 第四条, Jdbcs类加载nutz_jdbc_experts.js完成的提示,这是各种数据库方言的配置文件
* 第五条, 第一次从数据库连接池获取连接的前置log, 如果数据库配置出错,网络不通等等问题, 后面就只有报错的log了
* 第六条, 驱动程序的版本
* 第七条, 数据库版本. 我现在比较习惯MariaDB, 基本用法与mysql无异.
* 第八条, 是资源扫描的log,在扫描那些bean带@Table注解, 触发这句log的代码是 ```Daos.createTablesInPackage(dao, "net.wendal.nutzbook", false);```
* 第九条, 是查询User表有多少记录, java语句是 ```dao.count(User.class)```

在第一次启动的时候(或之后需要清除数据库的时候), 会有建表,插入之类的语句.