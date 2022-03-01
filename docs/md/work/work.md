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



# MySql日期

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



# Git基本命令

1.查看已配置的信息

```
git config --global --list
```

2.打开git bash工具配置git的user name和email，用于身份验证，依次输入：

```
git config --global user.name "your name"
git config --global user.email "your email"
```

3.执行以下语句来判断是否已经存在本地公钥

```
cat ~/.ssh/id_rsa.pub
```

4.生成公钥ssh key

```
ssh-keygen -t rsa -C "shenjianhong"
```

5.获取生成的公钥

```
cat ~/.ssh/id_rsa.pub
```

下载项目的最新更改，用于拉取某分支的最新副本（建议工作时每次都输入这个命令）(远端: origin) (分支名称: 可以是"master"或者是一个已经存在的分支)。

```
git pull 远端 分支名称 -u
```

pull出现refusing to merge unrelated histories，可以在pull命令后紧接着使用`--allow-unrelated-history`选项来解决问题（该选项可以合并两个独立启动仓库的历史）

浏览您所做的更改

```
git status
```

将更改加入到本次提交

当输入"git status"时，您的更改会显示为红色。

```
git add 红色的修改
git commit -m "提交的描述"
```

提交您的更改到服务器

```
git push 远端 分支名称
```

删除代码库的所有更改（包含未跟踪的文件）

```
git clean -f
```

将某分支合并到master分支

```
git merge 分支名称
```

克隆远程仓库到本地指定目录

```
git clone https://gitee.com/shenyiwu/test.git ./
```

添加本地文件

```
git add a.text
git commit -m "a text commit"
```



```
1.克隆远程仓库到本地
git clone https://gitee.com/shenyiwu/test.git ./

2.获取远程origin/master分支与当前分支合并
git pull origin master

3.将本地的 master 分支推送到 origin 主机的 master 分支
git push origin master
```

获取当前机器RSA秘钥：ssh-keygen -t rsa -C "自定义名称"