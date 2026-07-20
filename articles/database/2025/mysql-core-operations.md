# 【MySQL基础】MySQL核心操作全解析

> 原文：[https://blog.csdn.net/2302_79751907/article/details/151073184](https://blog.csdn.net/2302_79751907/article/details/151073184)  
> 作者：意疏｜许可：CC BY-SA 4.0

### 前言

你可能没意识到，平时刷手机时看到的聊天记录、购物订单、游戏角色信息，背后都藏着 “数据库” 在帮忙管理。而 MySQL，就是最常用的数据库工具之一，它像个 “智能文件柜”，能把杂乱的数据整理得井井有条，还能快速找到我们需要的信息。​

刚开始接触 MySQL 时，不少人会怕 “操作复杂”“看不懂代码”。其实不用慌，这部分内容会避开难懂的专业术语，从最实用的基础操作讲起 —— 比如怎么把数据存进 MySQL，怎么快速找出想要的信息，每一步都尽量简单明了。哪怕你是第一次碰数据库，跟着步骤慢慢试，也能很快上手，让你感受到 MySQL 管理数据的方便～

‼️没安装MySql请看👇👇👇：从下载到运行：MySQL 详细安装配置完整教程

### 一、数据库操作😶‍🌫️

我们先输入打开mysql

```
mysql -u root -p
```

###### 1.1 查看数据库🔍

1）查看MySQL服务器中所有数据库 通过以下SQL语句可列出当前MySQL服务下已存在的所有数据库：

```
SHOW DATABASES;
```

具体实操效果如下：

其中4个默认系统数据库的作用需重点了解：

- information_schema：MySQL的数据字典，记录所有数据库、表的结构及字段信息。
- performance_schema：性能监控库，存储服务器运行时的性能参数与状态。
- mysql：核心管理库，保存用户权限、系统配置等关键信息（如root用户密码）。
- sys：辅助管理库，包含预定义的存储过程和函数，简化日常运维操作。

注意：这4个数据库是MySQL安装后自动生成的核心组件，切勿随意删除或修改，否则可能导致服务器无法正常运行。

2）查看指定数据库的创建信息 若需了解某数据库的创建语句（如字符集、校对集），可使用以下命令：

```
SHOW CREATE DATABASE 数据库名称;
```

以查看sys数据库为例，实操效果如下：

```
SHOW CREATE DATABASE sys;
```

该命令会显示数据库的创建SQL语句，以及默认字符集等配置，便于后续复现或修改数据库属性。

3）查看当前正在操作的数据库 若忘记当前处于哪个数据库上下文，可通过以下命令查询：

```
SELECT DATABASE();
```

具体实操效果如下：注意：执行该命令前必须先通过USE语句选择数据库，否则会返回NULL（未选中任何数据库）。

###### 1.2 创建数据库➕

创建数据库的基本语法如下，其中可选参数可按需添加：

```
CREATE DATABASE [IF NOT EXISTS] 数据库名称 [库选项];
```

关键说明：

- IF NOT EXISTS：可选参数，意为“若数据库不存在则创建”，避免因重复创建导致报错。
- 数据库名称规则：仅允许包含字母、数字和下划线，且不能以数字开头（如db_test合法，123_db不合法）。
- 库选项：常用CHARSET（指定字符集）和COLLATE（指定校对集），默认字符集为latin1（不支持中文），建议显式设置为utf8mb4（支持中文及emoji等4字节字符，比utf8更全面）。

具体实操效果如下：

###### 1.3 选择数据库📌

在操作数据表或数据前，需先指定要操作的数据库，语法如下：

```
USE 数据库名称;
```

具体实操效果如下：

###### 1.4 删除数据库❌

删除数据库的语法如下，执行后会彻底清除数据库及其中所有数据，需谨慎操作：

```
DROP DATABASE [IF EXISTS] 数据库名称;
```

关键说明：

- IF EXISTS：可选参数，若数据库不存在则忽略删除操作，避免报错。
- 操作风险：删除数据库会永久删除其中所有数据表和数据，且无法恢复，建议操作前备份重要数据。

具体实操效果如下：

### 二、数据表操作📋

###### 2.1 创建数据表➕

创建数据表需基于已选中的数据库，基本语法如下，可按需配置字段、属性及表选项：

```
CREATE [TEMPORARY] TABLE [IF NOT EXISTS] 表名( 
 字段1 字段1类型 [字段属性] [COMMENT 字段1注释], 
 字段2 字段2类型 [字段属性] [COMMENT 字段2注释], 
 ...... 
 字段n 字段n类型 [COMMENT 字段n注释] 
) [表属性] [COMMENT 表注释];
```

关键说明：

- TEMPORARY：创建临时表，仅在当前MySQL会话中可见，会话关闭后自动删除。
- 字段类型：需根据数据特点选择（如INT存整数、VARCHAR存字符串、DATE存日期）。
- 字段属性：常用NOT NULL（非空约束）、DEFAULT（默认值）、PRIMARY KEY（主键）等。
- 表属性：常用ENGINE（存储引擎，推荐InnoDB，支持事务和外键）、DEFAULT CHARSET（字符集，建议设为utf8mb4），确保表支持中文及特殊字符。

具体实操效果如下： 首先创建一个数据库：CREATE DATABASE IF NOT EXISTS CompanyDB; 进入创建的数据库；USE CompanyDB;

```
CREATE TABLE IF NOT EXISTS Employee(
 emp_id INT PRIMARY KEY AUTO_INCREMENT COMMENT '员工ID：自动生成，每个员工唯一',
 emp_name VARCHAR(50) NOT NULL COMMENT '员工姓名：比如“张三”，必须填',
 emp_job VARCHAR(50) COMMENT '员工职位：比如“程序员”，可填可不填',
 emp_hire_date DATE COMMENT '入职日期：比如“2024-01-15”，可填可不填'
) COMMENT '最简单员工表：存员工核心信息';
```

👉显示ok即创建成功

###### 2.2 查看数据表🔍

1）查看当前数据库中的所有数据表 语法如下，可选LIKE匹配模式筛选表名：

```
SHOW TABLES [LIKE 匹配模式];
```

匹配模式说明：

- %：匹配任意长度的字符（包括0个），如SHOW TABLES LIKE 'user%'匹配所有以user开头的表。
- _：仅匹配1个字符，如SHOW TABLES LIKE 'user_'匹配user1、userA等（仅后缀1个字符）。

具体实操效果如下：

2）查看数据表的详细信息 若需了解表的存储引擎、创建时间、字符集等信息，可使用以下命令：

```
SHOW TABLE STATUS [FROM 数据库名] [LIKE 匹配模式];
```

具体实操效果如下：扩展技巧：在命令末尾加\G可将结果纵向排列，便于查看字段较多的表信息（如大表的存储大小、行数）。

###### 2.3 查看表结构📊

MySQL提供多种方式查看表结构，核心是了解字段名、类型、约束等信息：

1）简洁查看字段信息（DESC/DESCRIBE） 两种语法效果一致，前者为后者的简写：

```
# 语法1：查看所有字段
{DESCRIBE|DESC} 数据表名;

# 语法2：查看指定字段
{DESCRIBE|DESC} 数据表名 字段名;
```

查看所有字段的实操效果如下：desc employee;

查看指定字段的实操效果如下： desc employee emp_id;

2）查看数据表的创建语句 若需复现表结构或查看完整配置（如存储引擎、字符集），可使用：

```
SHOW CREATE TABLE 表名;
```

具体实操效果如下： SHOW CREATE TABLE employee/G;

3）详细查看字段属性（SHOW COLUMNS） 添加FULL参数可查看字段权限、校对集等额外信息：

```
# 语法1：基于当前数据库
SHOW FULL COLUMNS FROM 数据表名;

# 语法2：查看指定数据表完整结构
SHOW [FULL] COLUMNS FROM 数据库名.数据表名;
```

查看完整信息的实操效果如下： SHOW FULL COLUMNS FROM Employee; 查看指定数据表完整结构：SHOW FULL COLUMNS FROM CompanyDB.Employee;

###### 2.4 删除数据表❌

删除数据表会彻底清除表结构及所有数据，语法如下：

```
# 单表删除（永久表）
DROP TABLE [IF EXISTS] 数据表名;
```

单表删除（永久表）的实操效果如下： deop table if exists employee;

### 三、数据操作🔄

###### 3.1 增加数据➕

MySQL提供多种数据插入方式，可按需选择单条、多条或指定字段插入：

1）为部分字段插入数据 适用于仅需赋值部分字段（未赋值字段需允许为空或有默认值），两种语法如下：

```
# 语法1：字段列表+VALUES
INSERT [INTO] 数据表名(字段1, 字段2, ...) {VALUES|VALUE} (值1, 值2, ...);

# 语法2：SET关键字赋值（灵活性更高）
INSERT [INTO] 数据表名 SET 字段1=值1, 字段2=值2, ...;
```

字段列表+VALUES的实操效果如下：

```
INSERT INTO Employee(emp_name, emp_job, emp_hire_date)
 -> VALUES('李四', NULL, NULL);
```

```
SELECT * FROM Employee;
```

SET关键字赋值的实操效果如下：

```
INSERT INTO Employee ​
SET emp_name='王五', emp_job='销售', emp_hire_date='2024-03-15';
```

```
SELECT * FROM Employee;
```

注意：字段顺序与值顺序必须一一对应，字符串类型的值需用单引号包裹（如'李四'）。

2）为所有字段插入数据 可省略字段列表，但值的顺序必须与表结构字段顺序完全一致：

```
INSERT [INTO] 数据表名 {VALUES|VALUE} (值1, 值2, ..., 值n);
```

具体实操效果如下：

```
INSERT INTO Employee VALUES(NULL, '周二', NULL, NULL);
```

```
SELECT * FROM Employee;
```

3）批量插入多行数据 通过逗号分隔多个值列表，大幅提升插入效率（避免多次执行单条插入）：

```
INSERT [INTO] 数据表名 [字段列表] VALUES (值列表1), (值列表2), ..., (值列表n);
```

具体实操效果如下：

```
INSERT INTO Employee (emp_name, emp_job, emp_hire_date)
VALUES 
 ('吴九', '产品经理', '2024-05-01'), -- 第一条：填全3个字段
 ('郑十', '设计师', NULL), -- 第二条：不填入职日期（用NULL）
 ('钱十一', NULL, '2024-05-10'); -- 第三条：不填职位（用NULL）
```

```
SELECT * FROM Employee;
```

###### 3.2 查询数据🔍

查询是数据操作的核心，支持查询所有字段、指定字段及带条件筛选：

1）查询表中所有数据 使用*通配符表示所有字段，适用于需查看完整数据的场景：

```
SELECT * FROM 数据表名;
```

具体实操效果如下：

2）查询指定字段数据 仅查询所需字段，减少数据传输量，提升效率：

```
SELECT 字段1, 字段2, ... FROM 数据表名;
```

具体实操效果如下：

```
SELECT emp_name, emp_job, emp_hire_date FROM Employee WHERE emp_job='产品经理';
```

3）带条件查询数据 通过WHERE子句筛选符合条件的记录，常用条件运算符（=、>、<、!=等）：

```
# 语法1：查询所有字段（带条件）
SELECT * FROM 数据表名 WHERE 条件表达式;

# 语法2：查询指定字段（带条件）
SELECT 字段1, 字段2 FROM 数据表名 WHERE 字段名=值;
```

带条件查询所有字段的实操效果如下：

```
SELECT * FROM Employee WHERE emp_job='产品经理';
```

带条件查询指定字段的实操效果如下：

```
SELECT emp_name, emp_hire_date FROM Employee WHERE emp_job='设计师';
```

###### 3.3 修改数据✏️

通过UPDATE语句修改已有数据，必须加WHERE条件（否则会修改表中所有记录）：

```
UPDATE 数据表名 SET 字段1=值1, 字段2=值2, ... [WHERE 条件表达式];
```

关键说明：

- 多字段修改用逗号分隔“字段=值”对。
- WHERE条件用于定位需修改的记录（如id=1），避免误改无关数据。

具体实操效果如下：

```
UPDATE Employee 
SET emp_job='高级销售' 
WHERE emp_name='王五';
```

```
SELECT * FROM Employee;
```

###### 3.4 删除数据❌

通过DELETE语句删除数据，同样必须加WHERE条件（否则会删除表中所有记录）：

```
DELETE FROM 数据表名 [WHERE 条件表达式];
```

关键说明：

- 若需清空表中所有数据且不保留表结构，也可使用TRUNCATE TABLE 表名（效率更高，但无法恢复数据，且不触发删除触发器）。
- DELETE支持带复杂条件删除（如WHERE age>30），需谨慎验证条件正确性。

具体实操效果如下：

```
DELETE FROM Employee WHERE emp_name='钱十一';
```

### 四、实用辅助操作🛠️

###### 4.1 查看MySQL安装目录📍

通过查询BASEDIR变量，可快速获取MySQL的安装路径（便于找到配置文件my.ini或my.cnf）：

```
SHOW VARIABLES LIKE 'BASEDIR';
```

具体实操效果如下：

###### 4.2 查看数据存储目录📍

通过查询DATADIR变量，可找到数据库文件的实际存储路径（如ibdata1共享表空间文件、各数据库对应的文件夹及表文件）：

```
SHOW VARIABLES LIKE 'DATADIR';
```

具体实操效果如下：

###### 4.3 查询错误日志目录📍

错误日志记录MySQL运行中的异常信息（如启动失败、SQL执行错误、连接超时等），通过以下命令可找到日志路径，便于排查故障：

```
SHOW VARIABLES LIKE 'log_error';
```

具体实操效果如下：

### 总结

以上就是MySQL基础操作的完整内容，确保新手实操时少踩坑。 如果在操作中遇到问题，欢迎在评论区留言或私信交流；若觉得内容对自己有帮助，不妨点赞、关注支持一下，后续会持续更新MySQL进阶教程（如索引优化、事务管理、多表关联查询），感谢大家的阅读！

---

意气风发，漫卷疏狂学习是成长的阶梯，每一次的积累都将成为未来的助力。我希望通过持续的学习，不断汲取新知识，来改变自己的命运，并将成长的过程记录在我的博客中。如果我的博客能给您带来启发，如果您喜欢我的博客内容，请不吝点赞、评论和收藏，也欢迎您关注我的博客。 您的支持是我前行的动力。听说点赞会增加自己的运气，希望您每一天都能充满活力！愿您每一天都快乐，也欢迎您常来我的博客。我叫意疏，希望我们一起成长，共同进步。 我是意疏 下次见！
