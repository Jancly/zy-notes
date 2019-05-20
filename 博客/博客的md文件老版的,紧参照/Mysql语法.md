---
title: 'Mysql语法 '
toc: true
tags:
    - 学习
    - mysql
---
>收到反馈回复的思念
<!-- more -->

# Mysql介绍
## 一，sql分类

1,**DDL**  数据定义语言 ：用来定义数据库对象（database,table);
2,**DML**  数据操作语言 ：用来对数据中表的记录进行更新（insert,delete,update);
3,**DQL**  数据查询     ：用来查询数据库中的记录( select,from,where);
4,**DCL**  数据控制语言 :(grent)

## 二，库操作
### 2.1启动mysql
**以下代码都是在cmd命令指示符或者在mysql中输入**
* 启动数据库
``` bash
net start mysql
```
* 输入密码
``` bash
mysql -u root -p
```
<!-- more -->
### 2.2创建库
* 创建库
``` bash
create database +(库名);
```
* 创建带有编码的库
``` bash
create database  +(库名) character set gbk/utf-8;
```
### 2.3查看数据库
* 查看所有数据库
``` bash
show databases;
```
* 查看某个数据库
``` bash
show create database +(数据库名);
```
### 2.4删除数据库
``` bash
drop database +(库名);
```
### 2.5查看正在使用的数据库
* 查看正在使用的数据库
``` bash
select database();
```
* 使用库
``` bash
use +(库名);
```
## 三，表操作
### 3.1 创建表
```bash
create table 表名（
        字段名  类型（长度） [约束]，
        字段名  类型（长度） [约束]，
        字段名  类型（长度） [约束]
        ）;
```
### 3.2 查看表
前提是要在某个数据库中使用次代码
* 查看所有表
``` bash
show  tables;
```
* 查看某一个表
``` 
show create table 表名;
```
* 查看表结构
``` 
desc 表名
```
### 3.3 表的修改
* 删除表格
```
drop table 表名
```
* 修改表的结构
1， 将表格增加一列
```
alter table 表名 add 字段名 类型（长度） [约束];
```
2，修改列的类型（长度，约束）
```
alter table 表名 modify 要修改的字段名 类型（长度） [约束];
```
3，修改列的列名
```
alter table 表名 change 旧列名 新列名 类型（长度） [约束];
```
4,删除表的列
```
alter table 表名 drop 列名
```
5，修改表的字符集
```
alter table 表名 character set 编码
```
## 四，DML 插入（insert)
### 4.1 插入记录
* 部分插入
```
insert into 表名（列名1，列名2，列名3...）values(值1，值2，值3...);
```
有多少个列名对应多少个值
* 全部插入
```
insert into 表名 values(值1，值2，值3...);
```
值对应所有的列名
### 4.2 插入时出现乱码
```
set name gbk;
```
### 4.1 修改(update)
* 不带条件的修改（全部修改）
```
update 表名 set 字段名='值'，字段名 ='值'...;
```
* 带条件修改
```
update 表名 set 字段名='值'，字段名 ='值'... where 条件（例:字段名='值'）；
```
### 4.1删除表记录
* 不带条件
```
delete from 表名 
```
* 带条件
```
delete from 表名 where 条件
```
* delete 与 truncate 的区别
delete ：删除的时候是一条条的删除记录 ，可以将数据找回。（不过我从未找回过）
truncate : 它是将整个表摧毁然后创建一模一样的表，它删除的数据无法找回。
找回的方法
start transaction  :开启新事务，可以回滚
rollback: 回滚
## 五，DQL 查询
### 5.1
* 查所有
```
select *from 表名;
```
* 查某一列
```
select 列名，列名  from 表名;
```
* 查所有使用别名
```
select *from 表名 as 别名;
```
* 查列使用列别名
```
select 列名 as 别名 from 表名;
```
### 5.2 去重复
```
select distinct 列名 from 表名;
```
### 5.3将列名+10进行显示
```
select 列名，列名+10 from 表名；
```
### 5.4条件查询
1，查询指定的列名值的信息
```
select *from 表名 where 列名='值';
```
2,查询列名值大于60的
```
select *from where 列名>60;
```
3,查询列名值含有某值
```
select *from 表名 where 列名 like '%值%';
```
4,查询列名值在某一范围如（3，6，9）
```
select *from 表名 where 列名 in (3,6,9);
```
5,多条件成立时
```
select *from 表名 where 列名.. and(or) 列名..;
```
## 六，排序
### 6.1 通过列名值升序
```
select *from 表名 order by 列名 asci;
```
### 6.2 通过列名值降序
```
select *from 表名 order by 列名 desc;
```
## 七，聚合函数（不统计null值）
### 7.1求总合·
```
select sum （列名） from 表名;
```
### 7.2求平均
```
select avg （列名） from 表名;
```
### 7.3求所有个数
```
select count(列名) from 表名;
```
## 八，分组操作
### 8.1 语法
```
select count *from 表名 group by 列名;
```
### 8.2 根据列名cid分组，分组计平均，并且平均大于20000
```
select avg（列名）from 表名 group by cid having avg(列名)>20000;
```
分组用having 不用where
## 九，总结及注意
## 语句顺序
select
from
where
group by
having :分组后带条件时只能用having
order by 最后
## 如果有其他补充下次来更新











