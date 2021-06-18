```sql
select 1 from t_score join t_course on t_score.course=t_course.course
-- 显示1字段 记录也是1 多少行呢，
-- 1，14row 笛卡尔积
-- 2，7row
-- 3，7row
-- 4，7row
-- 5，14row
```

> 左连接 以左表为主查右表 没有数据以null填充

```sql
-- 对学生成绩分科目进行排名，相同分数按学号id排名
select id,course,score,row_number(partition by score order by score desc,id) 排名
form t_score
```

![image-20210607100502087](C:\Users\pflong\AppData\Roaming\Typora\typora-user-images\image-20210607100502087.png)

导入sql数据到数据库

```shell
mysql -uroot -p shcool < data.sql
```



## MySQL分区 （partition）功能

### 水平分区的模式：

1. **Range（范围）** – 这种模式允许DBA将数据划分不同范围。例如DBA可以将一个表通过年份划分成三个分区，80年代（1980's）的数据，90年代（1990's）的数据以及任何在2000年（包括2000年）后的数据。 
2. **Hash（哈希）** – 这种模式允许DBA通过对表的一个或多个列的Hash Key进行计算，最后通过这个Hash码不同数值对应的数据区域进行分区。例如DBA可以建立一个对表主键进行分区的表。 
3. **Key（键值）**  – Hash模式的一种延伸，这里的Hash Key是MySQL系统产生的。 
4. **List（预定义列表）** – 这种模式允许系统通过DBA定义的列表的值所对应的行数据进行分割。例如：DBA建立了一个横跨三个分区的表，分别根据2004年2005年和2006年值所对应的数据。 

### 垂直分区（按列分）：

​    举个简单例子：一个包含了大text和BLOB列的表，这些text和BLOB列又不经常被访问，这时候就要把这些不经常使用的text和BLOB了划分到另一个分区，在保证它们数据相关性的同时还能提高访问速度。

