# mysql知识巩固与完善（注意我后面带分号的一定要加上）

##  1. 登入数据端与基本操作：

 1. 在命令行输入：***mysql -h localhost -P 3306 -u root -proot***（注意密码这里没有空格）进入客户端，进行简写：PS C:\Users\有天道> ***mysql -u root -p***。

 2. 在命令行输入： ***exit*** 退出客户端 ，输入*** select version();***显示浏览器版本。

 3. ***show databases;***使用这个指令可以查看所有数据库。

    <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210915225825317.png" alt="image-20210915225825317" style="zoom:50%;" />

 4. ***use***+指定数据库名称—>打开数据库。

    ![image-20210915230241417](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210915230241417.png)

 5. 打开一张表***show table***

    ![image-20210915230437383](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210915230437383.png)

 6. ***desc 表名;***查看表的结构

    <img src="https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20210915230948537.png" alt="image-20210915230948537" style="zoom:50%;" />

    

    ~~~sql
    使用 DISTINCT 关键字
    SELECT DISTINCT 列名称 FROM 表名称
     
    ~~~




## 2. 基本操作

1. 历史
2. sql被分为三个方面，分别为数据定义语言**DDL** 、数据操作语言**DML**、 数据控制语言**DCL**。

**数据定义语言DDL**：

> create(创建) alter(修改) drop(降低) rename truncate

**数据操作语言DML**:

> insert delete  update

**数据控制语言DCL**:

> 提交对于数据的修改:commit
>
> 返回上一次修改:rollback
>
> 设置一个保存点:savepoint
>
> 设置相关权限：grant
>
> 回收相关权限：revoke

3. 基本指令的使用：

+ 使用命令行的方式导入数据库：

~~~sql
source 文件路径	
~~~

+ 使用命令行的方式查看所有数据库：

~~~sql
show databases
# 查询结果
+--------------------+
| Database           |
+--------------------+
| account            |
| aoteman            |
| cyh_database       |
| information_schema |
| jinlingdata        |
| kdyg               |
| mall               |
| mysql              |
| news               |
| performance_schema |
| sakila             |
| shoops             |
| shopping           |
| use                |
| xiaoshuo           |
| yt                 |
| yu                 |
| 口袋妖怪            |
| 奥特曼             |
| 奥特曼写作系统     |
| 收入与支出         |
| 杨腾的基本信息     |
| 皇帝养成计划       |
+--------------------+
~~~

+ 使用`show tables`可以查看该数据库下面的所有表：

~~~sql
+------------------------+
| Tables_in_cyh_database |
+------------------------+
| aoteman_table          |
| books_table            |
| caiyuhao               |
| chapter                |
| user_table             |
| 最初的精灵表           |
| 玩家精灵表             |
| 精灵表                 |
+------------------------+
~~~

+ 使用列的别名，其实是可以带空格，但是要这么写,注意这使用别名里面用双引号：

~~~sql
SELECT `name` "姓名" FROM `user_table`;
-- 使用特殊方式为列赋值别名
SELECT `name` "user name" FROM `user_table`;
~~~

![image-20211206104742936](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211206104742936.png)

![image-20211206104818902](https://gitee.com/theCompassWillAlsoGetLost/typora-picture-resources2/raw/master/img/image-20211206104818902.png)

+ 加在前面`distinct`（不同的）关键字可以去掉重复的行数，写两个字段名在该字段后面，表示整体三没有重复名
+ 使用`ISNULL(判断不为空的值，判断为空的值)`
+ 注意如果需要查询字段为null的数据，直接写`字段名=null`是没有用的，需要加上`字段名<=>null` 这样的返回结果才为真
+ sql里面的like模糊查询

| 前面的个数不确定                       | 前面的个数确定                    |
| -------------------------------------- | --------------------------------- |
| like '%a%'                             | like '_a%'                        |
| like '%a%b%' 同时包含ab的字符          | like '__a'这就是表示第三个字符为a |
| like '_\ __'这个表示第一个字符就是 '_' |                                   |

