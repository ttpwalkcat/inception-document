#发布日志
###2015年10月26日Inception2.1.17发布
1. [**新增**]新增inception get osc processlist的功能，这个语句可以查看所有当前正在执行的OSC线程。
2. [**新增**]新增inception get processlist的功能，这个语句可以查看所有当前正在执行的线程。
3. [**新增**]新增参数inception_osc_recursion_method，可以配置在执行OSC时，因为从库有延迟，或者复制停止导致不能正常执行OSC时，可以设置这个参数为NONE跳过slave的检查。
4. 修改在timestamp类型的列设置默认值为合法的日期，但不在其合法范围内没有报错的问题。
5. 修改回滚语句拼写错误的问题（多了一个AND）
6. 修改在只读模式下、不是执行模式的情况下，没有填备份信息还报非法备份的问题
7. 修改time类型的列建表指定默认值时，报非法默认值的问题
8. 修改在不同数据库下，执行相同的ALTER表时，生成的sha1是一样的，导致在获取进度时不准确的问题
9. 修改在生成drop index回滚语句时，ADD INDEX后面的列存在语法错误的问题
10. 修改在生成回滚语句时，注释太长导致栈溢出的问题

###2015年9月18日Inception2.1.9发布
1. [**新增**]新增参数inception_check_identifier
2. [**新增**]加入打印执行计划的功能
3. 修改在打印及审核表达式时字符串溢出导致内存覆盖的问题
4. 修改在多个加列并且有AFTER的时候，代码变量没有重置导致检查失败的问题
5. 对增删改查语句中的表达式检查的重构，不会漏掉一个表达式，检查更彻底，在Inception中一个比较遗憾的工作终于搞定了。
6. 修改Inception在启动的时候，错误的加载了非Inception配置文件组导致启动不成功的问题
7. 修改对时间类型默认值的检查，不考虑线上sql_mode值，只要是非法的时间值，都报警,时间类型包括所有的DATE、DATETIME、TIMESTAMP，默认值包括INT，STRING及DECIMAL等
8. 修改在处理sqlmode时代码错误导致系统崩溃的问题
9. 修改在回滚语句很长时，回滚表对应的字段为TEXT，导致语句被截断的问题，已经修改为Medium类型的TEXT。
10. 修改在生成回滚语句时，当主键不在第一个列时导致生成的语句存在语法错误的问题。
11. 废弃参数inception_ddl_support，请更新之后，不要再使用，已经不起作用了（之前手册也没有出现过，可以忽略）

###2015年8月28日Inception2.0.18-beta发布
1. 修改在binlogformat已经是ROW的情况下，还去设置，导致有些没有super权限时出错的问题
2. 修改在创建索引时，索引列为前缀索引时，没有考虑前缀长度，导致报大于767的问题
3. 加入对非法时间值在创建表及更改表时，没有报错的问题
4. 修改oSC执行时结果集名字错误的问题
5. 修改在截取alter table 真正修改的内容时，如果有注释内容，会出错的问题

###2015年8月3日Inception2.0.13-beta发布
1. 新增使用event对象的检查
2. 修改多表更新时，审核通过，执行失败的问题
3. 在表列定义为int(2)类似的情况下，会导致在设置Binlog解析记录长度时错误导致内存correption的问题
4. 在解析binlog出错之后，没有再去dump导致直接读取网络引起一直阻塞的问题
5. 修改对线上数据库操作时，数据库名字没有加"\`"导致报错的问题
6. 修改设置BLOB/TEXT为NOT NULL时报错级别为警告
7. 禁止在语句中直接使用@uservar类型的表达式
8. 修复Inception备份时Binlog解析错乱的问题
9. 增加对创建索引及新建表中，索引长度超过767的检查
10. 修改在生成ALTER回滚语句出错的问题

###2015年6月1日Inception2.0.3-beta发布
新增：  
1. 实现OSC执行的取消功能  
2. 在审核前获取一些线上参数来辅助审核，比如参数：explicit_defaults_for_timestamp
修复：  
1. 在Inception没有dump binlog权限的情况下，备份时Inception会陷入死循环的问题  

###2015年5月22日Inception2.0.0-beta发布