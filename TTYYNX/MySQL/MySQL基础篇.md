---
number headings: auto, first-level 1, max 6, start-at 1, _.1.1.
---
# 一、MySQL安装 
[安装教程](https://blog.csdn.net/weixin_47406082/article/details/131867849?spm=1001.2014.3001.5502)

# 二、基础内容

## 1. 数据模型

关系型数据库

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1695799663800-f3f0fa7c-195d-4778-a703-a10d5fd2ac04.png)

## 2. SQL语句

1. 通用语法

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1695799921934-74d9c33d-861f-41e3-bcc8-ec1d572b4d4a.png)

2. 语句分类

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1695800170547-fe9577d1-26fe-49e8-9b2b-b707cc744d72.png)

### 2.1. DDL

show databases; 查询所有数据库

select database; 查询当前数据库

create database 数据库名； 创建数据库

drop database 数据库名; 删除数据库

use 数据库名; 使用数据库

#### 2.1.1. 表的创建&查询

##### 2.1.1.1. 查询当前数据库的所有表

show tables;

##### 2.1.1.2. 查询表结构

desc 表名;

##### 2.1.1.3. 查询指定表的建表语句

show create table 表名;

##### 2.1.1.4. 建表语句

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696404830082-8ab5680f-39ac-4880-8f41-0c161f5805d3.png)

注意最后一个字段没有逗号。

#### 2.1.2. 数据类型

##### 2.1.2.1. 数值类型

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696408133287-f9bc9342-c319-42f4-9f89-e796680edac4.png)

##### 2.1.2.2. 字符串类型

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696408206502-c38f4df6-8657-428c-a92d-e980e2737714.png)

##### 2.1.2.3. 日期时间类型

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696408233616-d34a3ed1-e4e1-48db-abf1-900889d13b30.png)

#### 2.1.3. 表的修改&删除

##### 2.1.3.1. 增加字段

alter table 表名 add 字段名 数据类型 [comment 注释]；

##### 2.1.3.2. 修改字段

1、修改数据类型

alter table 表名 modify 字段名 新数据类型;

2、修改字段名和字段类型

alter table 表名 change 旧字段名 新字段名 数据类型 [comment 注释];

##### 2.1.3.3. 删除字段

alter table 表名 drop 字段名;

##### 2.1.3.4. 表名修改

alter table 表名 rename to 新表名

##### 2.1.3.5. 删除表

drop table 表名;

truncate table 表名; （此语句会先将表删除，再重建一个一样的，不过数据会被清空）

### 2.2. 图形化界面工具DataGrip

#### 2.2.1. 教程
[下载及其基本使用教程](https://blog.csdn.net/m0_70536638/article/details/128860243?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169657362816800192218937%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=169657362816800192218937&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_click~default-2-128860243-null-null.142%5Ev94%5Einsert_down28v1&utm_term=datagrip&spm=1018.2226.3001.4187)

### 2.3. DML

#### 2.3.1. 表中添加数据

##### 2.3.1.1. 给表中指定字段添加数据

insert into 表名(字段1,字段2,........) values (值1,值2,.......);

##### 2.3.1.2. 给全部字段添加值

insert into 表名 values(值1,值2,.......);

##### 2.3.1.3. 批量添加值

insert into 表名(字段1,字段2,........) values （值1,值2,.......),(值1,值2,......),(值1,值2,......);

insert into 表名 values（值1,值2,.......),(值1,值2,......),(值1,值2,......);

##### 2.3.1.4. 添加数据注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696596757372-bed8755d-ebe7-4ab1-b5f8-fe32e4b2238b.png)

#### 2.3.2. 表中更新数据

update 表名 set 字段名1 = 值1,字段名2 = 值2,.......[where 条件]；

where条件语句可有可无，where语句若是没有，则表的上述字段的数据都会更新。

#### 2.3.3. 表中删除数据

delete from 表名[where 条件];

where条件语句可有可无，where语句若是没有，表中的数据都会被删除。

若需要单独删除，可以借助update。

### 2.4. DQL

#### 2.4.1. 语法

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696599689196-2ad72713-716b-47bd-bff9-a3d053ca8261.png)

#### 2.4.2. 基础查询

##### 2.4.2.1. 查询指定字段

select 字段1, 字段2, 字段3...from 表名;

##### 2.4.2.2. 查询所有字段

select 字段1, 字段2,... 字段n from 表名;

##### 2.4.2.3. 查询某一字段起别名

select 字段名 (as) 'xxx' from 表名;

as 可写可不写

##### 2.4.2.4. 查询某一字段不要重复

select distinct 字段名 from 表名;

#### 2.4.3. 条件查询

##### 2.4.3.1. 语法和条件

语法: **select 单/多个字段 from 表名 where 条件**;

条件解释如下：

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696735315030-db6afb55-7360-4fad-93f6-7e4f4077d5ff.png)

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696735350741-eb8f5c30-10a9-46ed-8fdd-bf33fec9a90e.png)

范例：

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696736123861-6eb604df-eaf3-48bd-8e92-90084dcdae6c.png)

#### 2.4.4. 聚合函数

##### 2.4.4.1. 语法以及常见的聚合函数

语法: **select 聚合函数(字段列表) from 表名;**

常见聚合函数：

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696817970486-20cbc606-49fe-49d3-a62e-654375119fcd.png)

##### 2.4.4.2. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696818691089-6a95ed40-6d7d-4d56-82ae-ad1ec2e1e5bb.png)

#### 2.4.5. 分组查询

##### 2.4.5.1. 语法

select 字段列表 from 表名 [where 条件] group by 分组字段名 [having 分组后过滤条件]

##### 2.4.5.2. having 和 where的区别

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696820510711-a0b177fc-0117-4515-840e-a973de7bd32f.png)

##### 2.4.5.3. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696820568309-cd5a3503-e52f-4d71-8963-3272774721c6.png)

##### 2.4.5.4. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696835212858-c7dcd0a3-db59-4c8b-a15c-fa81c429405e.png)

#### 2.4.6. 排序查询

##### 2.4.6.1. 语法

select 字段列表 from 表名 order by 字段1 排序方式1,字段2 排序方式2;

##### 2.4.6.2. 排序方式

asc 升序 （可省略，默认是升序）

desc 降序

##### 2.4.6.3. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696835686533-eba5d617-7cd1-4d87-9d0c-e4794a440ebc.png)

##### 2.4.6.4. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696836137122-3ac2fe63-041b-495e-92d1-b8607c27cdb7.png)

#### 2.4.7. 分页查询

##### 2.4.7.1. 语法

select 字段列表 from 表名 limit 起始索引，查询记录数;

##### 2.4.7.2. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696836593433-88c818f4-88b4-4ec4-9711-4a0f5f7bfa15.png)

##### 2.4.7.3. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696836849878-31098eaf-2d90-487b-9889-6fc809a2db52.png)

#### 2.4.8. 编写与执行顺序

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696857613349-bd236bd2-cb3e-4296-b40f-1bd7ba207532.png)

### 2.5. DCL

#### 2.5.1. 管理用户

##### 2.5.1.1. 查询用户

use mysql;

select * from user;

##### 2.5.1.2. 创建用户

create user '用户名' @ '主机名' identified by '密码';

##### 2.5.1.3. 修改用户密码

alter user '用户名' @ '主机名' identified with mysql_native_password by '新密码';

##### 2.5.1.4. 删除用户

drop user '用户名' @ '主机名';

##### 2.5.1.5. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696861202119-ce858c57-f904-4b8c-9919-2f457c15237d.png)

#### 2.5.2. 权限控制

##### 2.5.2.1. 查询权限

show grants for '用户名' @ '主机名';

##### 2.5.2.2. 授予权限

grants 权限列表 on 数据库名.表名 to '用户名' @ '主机名';

##### 2.5.2.3. 撤销权限

revoke 权限列表 on 数据库名.表名 from '用户名' @ '主机名';

##### 2.5.2.4. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696862443389-c5922b35-3fa2-4509-95cf-9ceab7e4d93a.png)

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696862342738-86c63a3a-18fd-4eff-845b-f2bbf9217231.png)

此章主要运维人员用的较多，开发了解即可。

## 3. 函数（常见）

### 3.1. 字符串函数

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696941510339-df2252b1-15a7-4fe2-b7a8-446c2d69ab0e.png)

#### 3.1.1. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696941582763-7656f0fe-1720-4aef-8e7c-8bebbbec5cb4.png)

### 3.2. 数值函数

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696944483684-4a7af953-9b2c-4afd-bb2e-1a4b9fc29e2a.png)

#### 3.2.1. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696944543988-98642566-3c0c-437a-bef3-41a12285baeb.png)

### 3.3. 日期函数

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696947703470-895ca2f3-0f55-4379-a9e6-57537bd6da03.png)

#### 3.3.1. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696947719444-5cd9ff24-9cab-4043-b8e5-63a96e01da71.png)

### 3.4. 流程函数

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696950317070-af5054e8-ddb6-456b-9559-0d76a947af06.png)

#### 3.4.1. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696950350299-0533a34e-453d-4095-aa99-f106604d9e6f.png)

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696950367382-beec159b-9b7e-4a73-8b8f-07c6a70cf794.png)

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696950377457-1a01a2d4-29be-4fb9-b3a1-e8422dacaffb.png)

## 4. 约束

^cb4bd6

### 4.1. 分类

^a19663

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696987917469-0d953888-c7e1-4e59-ad1e-8a8be5761445.png)

### 4.2. 范例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697032345597-a6c4a8f8-0b53-4b16-8a89-a28004c2b882.png)

### 4.3. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697032208140-69eb6112-267d-41a2-8a7e-a9fc0f37f6e0.png)

### 4.4. 外键约束

^f7c1dd

#### 4.4.1. 语法

alter table 表名 add constraint 外键名称 foreign key (外键字段名) reference 主表(主表列名); -- 添加外键

alter table 表名 drop foreign key 外键名称; -- 删除外键

#### 4.4.2. 外键的删除更新行为

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697120858139-b4f9649b-edca-4ea5-94f5-113cba673dbb.png)

alter table 表名 add constraint 外键名称 foreign key(外键字段名) reference 主表(主列表名) on update cascade on delete cascade;

alter table 表名 add constraint 外键名称 foreign key(外键字段名) reference 主表(主列表名) on update set null on delete set null;

#### 4.4.3. 实例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697118894378-596d646a-9e31-4737-87a1-72e384b6287a.png)

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697120889943-10edcffe-728f-40f0-86fa-57e0142c2c44.png)

## 5. 多表查询

### 5.1. 多表关系

#### 5.1.1. 一对多
在一的那一方设立外键，例如部门和员工，员工的表设立外键去关联部门那张表。示例如下：
![[Pasted image 20231024154526.png]]

#### 5.1.2. 多对多
需要中间表，通过中间表引入外键来控制多对多关系，着重理解外键的作用[[MySQL基础篇#^a19663|外键约束的作用]]

示例代码:
```
create table student(  
    id int auto_increment primary key comment '主键ID',  
    name varchar(10) comment '姓名',  
    no varchar(10) comment '学号'  
) comment '学生表';  
  
insert into student(id, name, no) VALUES  (null, '黛绮丝', '2000100101'),(null, '谢逊', '2000100102'),(null, '殷天正', '2000100103'),(null, '韦一笑', '2000100104');  

create table course(  
    id int auto_increment primary key comment '主键ID',  
    name varchar(10) comment '课程名称'  
) comment '课程表';  
  
insert into course values (null, 'Java'), (null, 'PHP'), (null , 'MySQL') , (null, 'Hadoop');  
  --外键约束--
create table student_course(  
    id int auto_increment primary key comment '主键ID',  
    student_id int not null comment '学生ID',  
    course_id int not null comment '课程ID',  
    constraint fk_course_id foreign key (course_id) references course(id),  
    constraint fk_student_id foreign key (student_id) references student(id)  
) comment '学生课程中间表';
```

#### 5.1.3. 一对一
通常有两张表（以用户表为例），一张表的信息较为基本，另外一张表较为详细，详细的那个表设有一个id字段且unique，将此字段设置外键绑定基本表。

示例代码:
```
create table tb_user(  
    id int auto_increment primary key comment '主键ID',  
    name varchar(20) comment '姓名',  
    age int comment '年龄',  
    gender char(1) comment '1:男,2:女',  
    phone char(11) comment '手机号'  
) comment '用户基本信息表';  
  
create table tb_user_edu(  
    id int auto_increment primary key comment '主键ID',  
    degree varchar(50) comment '学历',  
    major varchar(50) comment '专业',  
    primaryschool varchar(50) comment '小学',  
    middleschool varchar(50) comment '中学',  
    university varchar(50) comment '大学',  
    userid int unique comment '用户ID',  
    constraint fk_userid foreign key (userid) references tb_user(id)  
) comment '用户教育信息表';
```
### 5.2. 多表查询概述
多表查询即在多张表中查询数据，往往需要加上一些约束条件。
#### 5.2.1. 笛卡尔积
指两个集合的所有组合情况，在多表查询中往往需要消除无效的笛卡尔积。







