# **PHP核心编程-day5**

每日目标

- 能够使用SQL语句查询数据
- 能够使用SQL语句添加数据
- 能够使用SQL语句删除数据
- 能够使用SQL语句修改数据



# 1. 关系型数据库

##   1.1 关系型数据库简介

案例: 创建一个数据表，能够保存学生的基本信息(学号、姓名、年龄等)和学生每一科的考试成绩

1)  一张表的形式

![img](assets/03.jpg) 

缺点: 重复数据太多（数据冗余）

 

2) 关系型数据库:

![1528187325051](assets/02.png)

 

缺点: 表多
优点:
   数据耦合性低
   每个数据表都能够独立管理





##   1.2 student 和 dept表

   目标: 创建student和dept表用来存储学生的基本信息、学院基本信息和学生所属的学院信息

![1534172874473](assets/04.png)



   student：学生表，所需字段  学号、姓名、性别、年龄、系别

```
create table student(
  sno int UNSIGNED auto_increment primary key,
  sname varchar(20) not null,
  sage tinyint UNSIGNED not null,
  sgender enum('男','女') not null,
  sdept tinyint UNSIGNED not null
)engine=myisam default charset=utf8;
```



   dept：系别表，所需字段  系号  系名

```
create table dept(
  dept_id tinyint UNSIGNED auto_increment primary key,
  dept_name varchar(20) unique not null
)engine=myisam default charset=utf8;
```



##   1.3 ali_admin、ali_cate和ali_article的关系

   目标: 创建 ali_cate表和ali_article表，用来保存栏目基本信息、文章信息 以及 作者、栏目、文章的关系

![05](assets/05.png)



ali_cate表（栏目表）： 栏目id (主键)、 栏目名、栏目别名、栏目创建时间

```
create table ali_cate(
  cate_id tinyint UNSIGNED auto_increment primary key,
  cate_name varchar(10) unique not null,
  cate_slug varchar(30) UNIQUE not null,
  cate_addtime date not null
)engine=myisam default charset=utf8;
```



ali_article（文章表）： 文章id（主键）、文章标题、文章内容、文章作者、所属栏目、发布时间、文章状态（草稿、已发布）

```
create table ali_article(
  article_id int UNSIGNED auto_increment primary key,
  article_title varchar(30) UNIQUE not null,
  article_content text not null,
  article_adminid int UNSIGNED not null,
	article_cateid tinyint UNSIGNED not null,
  article_addtime int not null,
  article_state enum('草稿','已发布')
)engine=myisam default charset=utf8;
```





# 2. **数据查询**

语法格式: 

SELECT  字段名1, 字段名2, ......

  FROM 表名	

​      [ WHERE <条件表达式> ]

​      [ ORDER BY <字段名> [ ASC|DESC ]]

​      [ LIMIT  START, LENGTH]

 

##  2.1 基本查询

格式:  select  字段名1, 字段名2,....  from  表名 

 案例1: 查询所有栏目的id和名称

 表:  ali_cate

 字段:  cate_id、cate_name

![1534213675206](assets/1534213675206.png)



 案例2: 查询管理员信息 (全部字段信息)

表: ali_admin

字段: 所有字段



方式一:  在select和from之间，列出所有字段

![1534213763761](assets/1534213763761.png)



方式二: 使用 * 来代表所有字段

![1534213822095](assets/1534213822095.png)





##  2.2 带where子句的查询

select  field1, field2... from 表名  查询表中的所有数据

  where 可以使用条件来筛选查询出的结果

![img](assets/01.jpg) 

 

案例3: 查询id值为2的栏目的所有信息

表: ali_cate

字段:  *

筛选条件:  cate_id = 2

![1534214952123](assets/1534214952123.png)



案例4: 查询年龄大于等于25的管理员的邮箱和昵称

表: ali_admin

字段:  admin_email、 admin_nickname

筛选条件:  admin_age >= 25

![1534215147258](assets/1534215147258.png)



案例5: 查询年龄在23-28之间的管理员的所有信息

表: ali_admin

字段: *

筛选条件： admin_age>=23  and  admin_age<=28



方法一:

![1534215257922](assets/1534215257922.png)



方式二:

![1534215324315](assets/1534215324315.png)



案例6: 查询年龄不在23-28之间的管理员的所有信息

表: ali_admin

字段: *

筛选条件： `admin_age<23  or  admin_age>28`

方法一:

![1534215426973](assets/1534215426973.png)



方法二：

![1534215454171](assets/1534215454171.png)



案例7: 查询年龄大于25的男性管理员信息

表: ali_admin

字段:  *

筛选条件:  admin_age>=25 and admin_gender='男'

![1534215590016](assets/1534215590016.png)



##  2.3 in关键词

集合:  一组相同类型的数据，使用()来包含，括号内使用 ， 分隔开

(1, 2, 3, 4, 5)  (‘潮科技’, ‘会生活’, ‘奇趣事’, ‘美奇迹’)  

 

案例8: 查询年龄为20、28的女性管理员信息

表： ali_admin

字段： *

筛选条件： admin_gender='女'  and  （admin_age=20 or admin_age=28）



方式一:

![1534215841500](assets/1534215841500.png)



方式二：

![1534215898938](assets/1534215898938.png)



##  2.4 模糊查询

通配符:

  %: 代表任意长度(包括0)的任意字符

  _:  代表1位长度的任意字符

​    a%b :  ab  abb  a对萨达b
    a_b: acb  atb  a的b
    a_b%:  acb  a&baaad

like: 在执行模糊查询时，必须使用like来作为匹配条件



案例9: 查询邮箱地址中包含字符h的管理员信息

表： ali_admin

字段： *

筛选条件： admin_email like '%h%'

![1534216354094](assets/1534216354094.png)



案例10: 查询包含“科技”关键词的文章信息

表： ali_article

字段： *

筛选条件：admin_title like ‘%科技%’

![1534216526440](assets/1534216526440.png)





案例11: 查询邮箱以a字符开头并且包含n的管理员信息

表： ali_admin

字段： *

筛选条件： admin_email like ‘a%n%’

![1534216625722](assets/1534216625722.png)





##  2.5 order by 排序

order by 可以对查询结果按某个字段的升降进行排序

  升序 asc （默认值） ，  降序 desc 

可进行排序的字段通常是  整型  英文字符串型  日期型  (中文字符串也行,但一般不用)



案例12: 查询所有的栏目信息，并按别名的降序排列

表： ali_cate

字段：*

排序条件： cate_slug  desc

![1534216794928](assets/1534216794928.png)



案例13: 查询所有栏目信息，并按发布时间升序排列

表：ali_cate

字段： *

排序条件：cate_addtime asc

![1534216877104](assets/1534216877104.png)



案例14: 查询所有男性的管理员信息，并按照创建时间降序排列

表： ali_admin

字段：*

筛选条件： admin_gender='男'

排序：admin_addtime desc

![1534217036912](assets/1534217036912.png)

 

##  2.6 limit 限制

limit用来限制查询结果的起始点和长度

 格式:  limit  var1, var2

 var1: 起始点。 查询结果的索引，从0开始。 0代表第一条数据

 var2: 长度

 

案例15: 查询年龄最大的3名男性管理员的信息

表： ali_admin

字段： *

筛选： admin_gender='男'

排序：order by admin_age desc

限制：limit 0,3



![1534218129029](assets/1534218129029.png)



案例16: 将文章按发布时间逆序排列，并取出第三条到第五条

表： ali_article

字段：*

排序： article_addtime desc

限制：limit 2,3

![1534218422235](assets/1534218422235.png)



将 *  解释成对应的字段需要 0.0001秒，但是人多了之后就会变慢。



##  2.7 多表查询

关键词: join   on

 

格式:  

select  *  from  表1

  join 表2  on  链接条件

链接条件一定是   表1的某个字段 =  表2的某个字段



案例: 查询学生的全部信息，系别需要使用系名来进行显示

表： student     dept

字段: student.*   dept.dept_name



![1534219437090](assets/1534219437090.png)





原理:

![1534219689703](assets/1534219689703.png)



案例17: 查询所有文章信息，作者使用昵称显示

表： ali_article   ali_admin

字段： ali_article.*   ali_admin.admin_nickname

![1534220115051](assets/1534220115051.png)



案例18: 查询大牛发布的所有文章信息，作者使用昵称显示

表： ali_article   ali_admin

筛选： admin_nickname='大牛'

![1534220239981](assets/1534220239981.png)



案例19: 查询属于潮科技和奇趣事的所有文章

表：ali_cate   ali_article

筛选条件： cate_name in ('潮科技', '奇趣事')

![1534220507814](assets/1534220507814.png)



案例20: 查询所有文章信息，作者使用昵称显示，栏目使用栏目名显示

表： ali_article    ali_admin   ali_cate

![1534220828795](assets/1534220828795.png)



 

# 3. 添加数据

# 4. 修改数据

格式:  

  update  表名   set   字段1=值1, 字段2=值2,...  where  修改条件

  修改表中的哪一条（几条）数据的 字段1=值1...

 

案例21: 将id为6的管理员昵称改为凯子





案例22: 将所有男性管理员的年龄都+1







# 5. **删除数据**

格式:  delete from 表名  where 删除条件

 

案例25: 删除cate_id=5的栏目


