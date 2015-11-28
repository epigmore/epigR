title: Oracle通过分区表曲线救国
date: 2015-11-25 19:09:30
categories: 程序开发
tags: Oracle
---

## 先提下我的业务需求：

> 有下属多个机构提供相同格式数据，汇总数据库要实现收集数据但又要保证各个机构数据的安全性（各机构不能互相查看数据）

环境：Oracle
提供基础数据表：

``` sql
create table msg_data (
	id varchar2(32) primary key,
	name varchar2(64),
	msg varchar2(255),
	phone varchar2(11),
	contentDesc varchar2(255)
)
```

## 初步拟定两种实现方案：

### 1）、视图
为机构obtain_01，obtain_02，obtain_03分别创建数据表，然后为所有表创建合并视图，基本能满足需求，汇总数据在视图中访问
语句如下

``` sql
create table msg_data_obtain_01 (
	id varchar2(32) primary key,
	name varchar2(64),
	msg varchar2(255),
	phone varchar2(11),
	contentDesc varchar2(255)
);

create table msg_data_obtain_02 (
	id varchar2(32) primary key,
	name varchar2(64),
	msg varchar2(255),
	phone varchar2(11),
	contentDesc varchar2(255)
);

create table msg_data_obtain_03 (
	id varchar2(32) primary key,
	name varchar2(64),
	msg varchar2(255),
	phone varchar2(11),
	contentDesc varchar2(255)
);

create view view_msg_data as
select t.*,'obtain_01' obtain from msg_data_obtain_01
union
select t.*,'obtain_02' obtain from msg_data_obtain_02
union
select t.*,'obtain_03' obtain from msg_data_obtain_03;
```

### 2）、分区表

创建列表分区，为每个分区创建视图授权给相对的用户

``` sql
create table msg_data (
	id varchar2(32) primary key,
	name varchar2(64),
	msg varchar2(255),
	phone varchar2(11),
	contentDesc varchar2(255),
	obtain varchar2(10)
)
partition by list(obtain)
(
	partition list_obtain_01 values('obtain_01'),
	partition list_obtain_02 values('obtain_02'),
	partition list_obtain_03 values('obtain_03')
);

create view view_msg_obtain_01 as
select * from msg_data partition(list_obtain_01);

create view view_msg_obtain_02 as
select * from msg_data partition(list_obtain_02);

create view view_msg_obtain_03 as
select * from msg_data partition(list_obtain_03);
```

## 对比：
用视图实现需求是最先想到的也最符合逻辑，后来需要操作汇总的数据，但是对于多张表的视图是无法直接执行增、删和改的操作的。只能通过创建视图的触发器才能完成需求。
用分区表实现的原因就是因为无法直接对汇总的数据进行增、删和改的操作，想到了列表分区的实现方式，一下所有问题都解决了。
（原创：转载请注明来源[http://epigmore.github.io/2015/11/25/Oracle/Oracle通过分区表曲线救国](http://epigmore.github.io/2015/11/25/Oracle/Oracle通过分区表曲线救国)）