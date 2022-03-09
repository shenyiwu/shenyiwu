# MySQL5.7
1.下载https://dev.mysql.com/downloads/mysql/

2.解压，然后在解压目录下创建my.ini,复制以下内容保存

```
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8

[mysqld]
# 设置3306端口
port = 3306 

# 设置mysql的安装目录
basedir=F:\mysql\mysql-5.7.35-winx64

# 设置mysql数据库的数据的存放目录
datadir=F:\mysql\mysql-5.7.35-winx64\data

# 允许最大连接数
max_connections=200

# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB
skip-grant-tables
```

3.环境变量Path中加入安装路径bin目录（F:\mysql\mysql-5.7.35-winx64\bin）

4.打开命令行窗口，进入到mysql安装目录

```
C:\Users\Administrator>F:

F:\>cd mysql\mysql-5.7.35-winx64\bin

F:\mysql\mysql-5.7.35-winx64\bin>
```

5.初始化，输入 mysqld --initialize
6.安装，输入 mysqld --install
7.启动，输入 net start mysql, 停止，net stop mysql
8.启动成功后，输入 mysql -u root -p 回车

9.输入 use mysql进入mysql数据库；

10.输入 update mysql.user set authentication_string=password('root') where user='root'; 设置数据库密码 适用于mysql 5.7版本；

11.将修改 mysql中的 my.ini文件，删掉最后一行的代码（跳过表验证）skip-grant-tables；

12.在cmd命令行窗口输入命令重启服务。



13.创建用户：CREATE USER 'erp_user'@'localhost' IDENTIFIED BY 'erp_user#%124579';

14.授权用户：GRANT ALL ON *.* TO 'erp_user'@'localhost';

15.刷新权限：FLUSH PRIVILEGES;



删除windows服务：

```
sc delete "服务名"
```

更改淘宝镜像：

```
npm config set registry https://registry.npm.taobao.org
```



group by 的sql查询时出现this is incompatible with sql_mode=only_full_group_by错误

解决方法

1.命令解决，执行以下命令

```
set @@GLOBAL.sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION;
```

2、修改 my.ini 文件

需修改mysql配置文件，通过手动添加sql_mode的方式强制指定不需要ONLY_FULL_GROUP_BY属性，

在 [mysqld] 下面添加代码：

```bash
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_ENGINE_SUBSTITUTION
```



MySql日期

```
MySQL自带的日期函数TIMESTAMPDIFF计算两个日期相差的秒数、分钟数、小时数、天数、周数、季度数、月数、年数，当前日期增加或者减少一天、一周等等。

SELECT TIMESTAMPDIFF(类型,开始时间,结束时间)
相差的秒数：

SELECT TIMESTAMPDIFF(SECOND,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的分钟数：

SELECT TIMESTAMPDIFF(MINUTE,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的小时数：

SELECT TIMESTAMPDIFF(HOUR,'1993-03-23 00:00:00 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的天数：

SELECT TIMESTAMPDIFF(DAY,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的周数：

SELECT TIMESTAMPDIFF(WEEK,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的季度数：

SELECT TIMESTAMPDIFF(QUARTER,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的月数：

SELECT TIMESTAMPDIFF(MONTH,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
相差的年数：

SELECT TIMESTAMPDIFF(YEAR,'1993-03-23 00:00:00',DATE_FORMAT(NOW(), '%Y-%m-%d %H:%i:%S'))
获取当前日期：

SELECT NOW()
SELECT CURDATE()
当前日期增加一天：

SELECT DATE_SUB(CURDATE(),INTERVAL -1 DAY)
当前日期减少一天：

SELECT DATE_SUB(CURDATE(),INTERVAL 1 DAY)
当前日期增加一周：

SELECT DATE_SUB(CURDATE(),INTERVAL -1 WEEK)
当前日期增加一月：

SELECT DATE_SUB(CURDATE(),INTERVAL -1 MONTH)

SELECT DATE_SUB(NOW(),INTERVAL -1 MONTH)
FRAC_SECOND  毫秒
SECOND  秒
MINUTE  分钟
HOUR  小时
DAY  天
WEEK  星期
MONTH  月
QUARTER  季度
YEAR  年
```

```
查看MySQL运行状态
show status 查看各种状态
show global status like 'uptime'; 查询当前MySQL本次启动后的运行统计时间
状态名	作用域	详细解释
Aborted_clients	Global	由于客户端没有正确关闭连接导致客户端终止而中断的连接数
Aborted_connects	Global	试图连接到MySQL服务器而失败的连接数
Binlog_cache_disk_use	Global	使用临时二进制日志缓存但超过binlog_cache_size值并使用临时文件来保存事务中的语句的事务数量
Binlog_cache_use	Global	使用临时二进制日志缓存的事务数量
Bytes_received	Both	从所有客户端接收到的字节数。
Bytes_sent	Both	发送给所有客户端的字节数。
com*		各种数据库操作的数量
Compression	Session	客户端与服务器之间只否启用压缩协议
Connections	Global	试图连接到(不管是否成功)MySQL服务器的连接数
Created_tmp_disk_tables	Both	服务器执行语句时在硬盘上自动创建的临时表的数量
Created_tmp_files	Global	mysqld已经创建的临时文件的数量
Created_tmp_tables	Both	服务器执行语句时自动创建的内存中的临时表的数量。如果Created_tmp_disk_tables较大，你可能要增加tmp_table_size值使临时 表基于内存而不基于硬盘
Delayed_errors	Global	用INSERT DELAYED写的出现错误的行数(可能为duplicate key)。
Delayed_insert_threads	Global	使用的INSERT DELAYED处理器线程数。
Delayed_writes	Global	写入的INSERT DELAYED行数
Flush_commands	Global	执行的FLUSH语句数。
Handler_commit	Both	内部提交语句数
Handler_delete	Both	行从表中删除的次数。
Handler_discover	Both	MySQL服务器可以问NDB CLUSTER存储引擎是否知道某一名字的表。这被称作发现。Handler_discover说明通过该方法发现的次数。
Handler_prepare	Both	A counter for the prepare phase of two-phase commit operations.
Handler_read_first	Both	索引中第一条被读的次数。如果较高，它建议服务器正执行大量全索引扫描；例如，SELECT col1 FROM foo，假定col1有索引。
Handler_read_key	Both	根据键读一行的请求数。如果较高，说明查询和表的索引正确。
Handler_read_next	Both	按照键顺序读下一行的请求数。如果你用范围约束或如果执行索引扫描来查询索引列，该值增加。
Handler_read_prev	Both	按照键顺序读前一行的请求数。该读方法主要用于优化ORDER BY ... DESC。
Handler_read_rnd	Both	根据固定位置读一行的请求数。如果你正执行大量查询并需要对结果进行排序该值较高。你可能使用了大量需要MySQL扫描整个表的查询或你的连接没有正确使用键。
Handler_read_rnd_next	Both	在数据文件中读下一行的请求数。如果你正进行大量的表扫描，该值较高。通常说明你的表索引不正确或写入的查询没有利用索引。
Handler_rollback	Both	内部ROLLBACK语句的数量。
Handler_savepoint	Both	在一个存储引擎放置一个保存点的请求数量。
Handler_savepoint_rollback	Both	在一个存储引擎的要求回滚到一个保存点数目。
Handler_update	Both	在表内更新一行的请求数。
Handler_write	Both	在表内插入一行的请求数。
Innodb_buffer_pool_pages_data	Global	包含数据的页数(脏或干净)。
Innodb_buffer_pool_pages_dirty	Global	当前的脏页数。
Innodb_buffer_pool_pages_flushed	Global	要求清空的缓冲池页数
Innodb_buffer_pool_pages_free	Global	空页数。
Innodb_buffer_pool_pages_latched	Global	在InnoDB缓冲池中锁定的页数。这是当前正读或写或由于其它原因不能清空或删除的页数。
Innodb_buffer_pool_pages_misc	Global	忙的页数，因为它们已经被分配优先用作管理，例如行锁定或适用的哈希索引。该值还可以计算为Innodb_buffer_pool_pages_total - Innodb_buffer_pool_pages_free - Innodb_buffer_pool_pages_data。
Innodb_buffer_pool_pages_total	Global	缓冲池总大小（页数）。
Innodb_buffer_pool_read_ahead_rnd	Global	InnoDB初始化的“随机”read-aheads数。当查询以随机顺序扫描表的一大部分时发生。
Innodb_buffer_pool_read_ahead_seq	Global	InnoDB初始化的顺序read-aheads数。当InnoDB执行顺序全表扫描时发生。
Innodb_buffer_pool_read_requests	Global	InnoDB已经完成的逻辑读请求数。
Innodb_buffer_pool_reads	Global	不能满足InnoDB必须单页读取的缓冲池中的逻辑读数量。
Innodb_buffer_pool_wait_free	Global	一般情况，通过后台向InnoDB缓冲池写。但是，如果需要读或创建页，并且没有干净的页可用，则它还需要先等待页面清空。该计数器对等待实例进行记数。如果已经适当设置缓冲池大小，该值应小。
Innodb_buffer_pool_write_requests	Global	向InnoDB缓冲池的写数量。
Innodb_data_fsyncs	Global	fsync()操作数。
Innodb_data_pending_fsyncs	Global	当前挂起的fsync()操作数。
Innodb_data_pending_reads	Global	当前挂起的读数。
Innodb_data_pending_writes	Global	当前挂起的写数。
Innodb_data_read	Global	至此已经读取的数据数量（字节）。
Innodb_data_reads	Global	数据读总数量。
Innodb_data_writes	Global	数据写总数量。
Innodb_data_written	Global	至此已经写入的数据量（字节）。
Innodb_dblwr_pages_written	Global	已经执行的双写操作数量
Innodb_dblwr_writes	Global	双写操作已经写好的页数
Innodb_log_waits	Global	我们必须等待的时间，因为日志缓冲区太小，我们在继续前必须先等待对它清空
原文地址		
Innodb_log_write_requests	Global	日志写请求数。
Innodb_log_writes	Global	向日志文件的物理写数量。
Innodb_os_log_fsyncs	Global	向日志文件完成的fsync()写数量。
Innodb_os_log_pending_fsyncs	Global	挂起的日志文件fsync()操作数量。
Innodb_os_log_pending_writes	Global	挂起的日志文件写操作
Innodb_os_log_written	Global	写入日志文件的字节数。
Innodb_page_size	Global	编译的InnoDB页大小(默认16KB)。许多值用页来记数；页的大小很容易转换为字节。
Innodb_pages_created	Global	创建的页数。
Innodb_pages_read	Global	读取的页数。
Innodb_pages_written	Global	写入的页数。
Innodb_row_lock_current_waits	Global	当前等待的待锁定的行数。
Innodb_row_lock_time	Global	行锁定花费的总时间，单位毫秒。
Innodb_row_lock_time_avg	Global	行锁定的平均时间，单位毫秒。
Innodb_row_lock_time_max	Global	行锁定的最长时间，单位毫秒。
Innodb_row_lock_waits	Global	一行锁定必须等待的时间数。
Innodb_rows_deleted	Global	从InnoDB表删除的行数。
Innodb_rows_inserted	Global	插入到InnoDB表的行数。
Innodb_rows_read	Global	从InnoDB表读取的行数。
Innodb_rows_updated	Global	InnoDB表内更新的行数。
Key_blocks_not_flushed	Global	键缓存内已经更改但还没有清空到硬盘上的键的数据块数量。
Key_blocks_unused	Global	键缓存内未使用的块数量。你可以使用该值来确定使用了多少键缓存
Key_blocks_used	Global	键缓存内使用的块数量。该值为高水平线标记，说明已经同时最多使用了多少块。
Key_read_requests	Global	从缓存读键的数据块的请求数。
Key_reads	Global	从硬盘读取键的数据块的次数。如果Key_reads较大，则Key_buffer_size值可能太小。可以用Key_reads/Key_read_requests计算缓存损失率。
Key_write_requests	Global	将键的数据块写入缓存的请求数。
Key_writes	Global	向硬盘写入将键的数据块的物理写操作的次数。
Last_query_cost	Session	用查询优化器计算的最后编译的查询的总成本。用于对比同一查询的不同查询方案的成本。默认值0表示还没有编译查询。 默认值是0。Last_query_cost具有会话范围。
Max_used_connections	Global	服务器启动后已经同时使用的连接的最大数量。
ndb*		ndb集群相关
Not_flushed_delayed_rows	Global	等待写入INSERT DELAY队列的行数。

Open_files	Global	打开的文件的数目。
Open_streams	Global	打开的流的数量(主要用于记录)。
Open_table_definitions	Global	缓存的.frm文件数量
Open_tables	Both	当前打开的表的数量。
Opened_files	Global	文件打开的数量。不包括诸如套接字或管道其他类型的文件。 也不包括存储引擎用来做自己的内部功能的文件。
Opened_table_definitions	Both	已经缓存的.frm文件数量
Opened_tables	Both	已经打开的表的数量。如果Opened_tables较大，table_cache 值可能太小。
Prepared_stmt_count	Global	当前的预处理语句的数量。 (最大数为系统变量: max_prepared_stmt_count)
Qcache_free_blocks	Global	查询缓存内自由内存块的数量。
Qcache_free_memory	Global	用于查询缓存的自由内存的数量。
Qcache_hits	Global	查询缓存被访问的次数。
Qcache_inserts	Global	加入到缓存的查询数量。
Qcache_lowmem_prunes	Global	由于内存较少从缓存删除的查询数量。
Qcache_not_cached	Global	非缓存查询数(不可缓存，或由于query_cache_type设定值未缓存)。
Qcache_queries_in_cache	Global	登记到缓存内的查询的数量。
Qcache_total_blocks	Global	查询缓存内的总块数。
Queries	Both	服务器执行的请求个数，包含存储过程中的请求。
Questions	Both	已经发送给服务器的查询的个数。
Rpl_status	Global	失败安全复制状态(还未使用)。
Select_full_join	Both	没有使用索引的联接的数量。如果该值不为0,你应仔细检查表的索引
Select_full_range_join	Both	在引用的表中使用范围搜索的联接的数量。
Select_range	Both	在第一个表中使用范围的联接的数量。一般情况不是关键问题，即使该值相当大。
Select_range_check	Both	在每一行数据后对键值进行检查的不带键值的联接的数量。如果不为0，你应仔细检查表的索引。
Select_scan	Both	对第一个表进行完全扫描的联接的数量。
Slave_heartbeat_period	Global	复制的心跳间隔
Slave_open_temp_tables	Global	从服务器打开的临时表数量
Slave_received_heartbeats	Global	从服务器心跳数
Slave_retried_transactions	Global	本次启动以来从服务器复制线程重试次数
Slave_running	Global	如果该服务器是连接到主服务器的从服务器，则该值为ON。
Slow_launch_threads	Both	创建时间超过slow_launch_time秒的线程数。
Slow_queries	Both	查询时间超过long_query_time秒的查询的个数。
Sort_merge_passes	Both	排序算法已经执行的合并的数量。如果这个变量值较大，应考虑增加sort_buffer_size系统变量的值。
Sort_range	Both	在范围内执行的排序的数量。
Sort_rows	Both	已经排序的行数。
Sort_scan	Both	通过扫描表完成的排序的数量。
ssl＊		ssl连接相关
Table_locks_immediate	Global	立即获得的表的锁的次数。
Table_locks_waited	Global	不能立即获得的表的锁的次数。如果该值较高，并且有性能问题，你应首先优化查询，然后拆分表或使用复制。
Threads_cached	Global	线程缓存内的线程的数量。
Threads_connected	Global	当前打开的连接的数量。
Threads_created	Global	创建用来处理连接的线程数。如果Threads_created较大，你可能要增加thread_cache_size值。缓存访问率的计算方法Threads_created/Connections。
Threads_running	Global	激活的（非睡眠状态）线程数。
Uptime	Global	服务器已经运行的时间（以秒为单位）。
Uptime_since_flush_status	Global	最近一次使用FLUSH STATUS 的时间（以秒为单位）。


查看系统变量及其值
show variables
show global variables like '%timeout'; 查询mysql连接超时

查看正在运行的线程
SHOW PROCESSLIST
```
