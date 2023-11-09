---
number headings: auto, first-level 1, max 6, start-at 1, _.1.1.
---
# 一、MySQL安装 
[安装教程](https://blog.csdn.net/weixin_47406082/article/details/131867849?spm=1001.2014.3001.5502)

# 二、基础内容
[视频教程](https://www.bilibili.com/video/BV1Kr4y1i7ru?p=1&vd_source=7664b55184fd63da03a03ef6c9be4310)

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

```SQL
use mysql;

select * from user;

```
##### 2.5.1.2. 创建用户

```SQL
create user '用户名' @ '主机名' identified by '密码';
```

##### 2.5.1.3. 修改用户密码

```SQL
alter user '用户名' @ '主机名' identified with mysql_native_password by '新密码';
```

##### 2.5.1.4. 删除用户

```SQL
drop user '用户名' @ '主机名';
```

##### 2.5.1.5. 注意事项

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1696861202119-ce858c57-f904-4b8c-9919-2f457c15237d.png)

#### 2.5.2. 权限控制

##### 2.5.2.1. 查询权限

```SQL
show grants for '用户名' @ '主机名';
```

##### 2.5.2.2. 授予权限

```SQL
grants 权限列表 on 数据库名.表名 to '用户名' @ '主机名';
```

##### 2.5.2.3. 撤销权限

```SQL
revoke 权限列表 on 数据库名.表名 from '用户名' @ '主机名';
```

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
``注：外键是用来控制数据库中数据的完整性的，就是当你对一个表的数操作时，和它关联的一个或多个表的数据同时发生改变。
#### 4.4.1. 语法

```SQL
alter table 表名 add constraint 外键名称 foreign key (外键字段名) reference 主表(主表列名); -- 添加外键

alter table 表名 drop foreign key 外键名称; -- 删除外键

```
#### 4.4.2. 外键的删除更新行为

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697120858139-b4f9649b-edca-4ea5-94f5-113cba673dbb.png)

语句如下：
```SQL
alter table 表名 add constraint 外键名称 foreign key(外键字段名) reference 主表(主列表名) on update cascade on delete cascade;

alter table 表名 add constraint 外键名称 foreign key(外键字段名) reference 主表(主列表名) on update set null on delete set null;
```

#### 4.4.3. 实例

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697118894378-596d646a-9e31-4737-87a1-72e384b6287a.png)

![](https://cdn.nlark.com/yuque/0/2023/png/39043900/1697120889943-10edcffe-728f-40f0-86fa-57e0142c2c44.png)

## 5. 多表查询
``注：
``1、在查询时，先思考问题涉及几个表，连接条件、查询条件又是什么。
``2、选择查询方式。若查询较复杂，那么在查询时分步操作。
``3、若需要查询n张表，那么连接条件至少会有n-1个条件，并且在梳理条件时，以两张表为单位去梳理。
### 5.1. 多表关系

#### 5.1.1. 一对多
在一的那一方设立外键，例如部门和员工，员工的表设立外键去关联部门那张表。示例如下：
![[Pasted image 20231024154526.png]]

#### 5.1.2. 多对多
需要中间表，通过中间表引入外键来控制多对多关系，着重理解外键的作用[[MySQL基础篇#^a19663|外键约束的作用]]

示例代码:
```SQL
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
```SQL
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
#### 5.2.2. 分类
![](Pasted%20image%2020231105111921.png)
### 5.3. 内连接
``注：
``1、通常当表名比较长时会起一个别名。
``2、在内连接中on和where没有区别。
#### 5.3.1. 隐式查询
```SQL
select 字段名1，字段名2…… from 表名1，表名2 where 条件
```
示例代码如下:
```SQL
-- 表 emp,dept
-- 连接条件:emp.dept_id  = dept.id  
  
-- 内连接隐式查询  
select e.name,d.name from emp e ,dept d where e.dept_id = d.id;
```
#### 5.3.2. 显式查询
```SQL
select 字段名1，字段名2…… from 表1 (inner) join 表2 on 条件
（其中inner可省略）
```
示例代码如下:
```SQL
-- 表 emp,dept
-- 连接条件:emp.dept_id  = dept.id

-- 内连接显式查询  
select e.name,d.name from emp e (inner) join dept d on e.dept_id = d.id;  
  
select e.name,d.name from emp e join dept d on d.id = e.dept_id;
```
### 5.4. 外连接
[on和where的区别](https://juejin.cn/post/6990283379841171493)
``注：在外连接中连接条件用On，查询条件用where。
#### 5.4.1. 左外连接
查询语法如下：
```SQL
select 字段1，字段2…… from 表1 left (outer) join 表2 on 连接条件 
```
作用范围是表1的全部内容以及表2和表1的交集
示例代码如下：
```SQL
-- 1.查询emp表的所有数据，和对应的部门信息(左外连接)  
-- 表 emp ，dept  
-- 条件 emp.dept_id = dept.id

-- 左外连接  
select e.*,d.name from emp e left (outer) join dept d on e.dept_id = d.id;  
  
select e.*,d.name from emp e left join dept d on e.dept_id = d.id;
```
#### 5.4.2. 右外连接
```SQL
select 字段1，字段2…… from 表1 right(outer) join 表2 on 条件
```
作用范围是表2的全部内容以及表1和表2的交集
示例代码如下:
```SQL
-- 2.查询dept表的所有数据，和对应的员工信息 
-- 表 emp ，dept  
-- 条件 emp.dept_id = dept.id

-- 右外连接  
select d.*,e.* from emp e right outer join dept d on e.dept_id = d.id;
```
### 5.5. 自连接
``根据需求自连接既可使用外连接的写法又可使用内连接的写法。
查询语法如下：
```SQL
select 字段1,字段2…… from 表T a,表T b where 条件(内连接写法);
select 字段1,字段2…… from 表T a left join 表T on 条件(外连接写法)
```
示例代码如下：
```SQL
-- 2.查询dept表的所有数据，和对应的员工信息  
-- 右外连接  
select d.*,e.* from emp e right outer join dept d on e.dept_id = d.id;  
  
-- 自连接  想象两张表的数据变化3D图像
-- 1、查询员工及其领导的名字 (内连接写法)  
select a.name,b.name from emp a, emp b where a.managerid = b.id;  
  
-- 2、查询所有员工emp及其领导名字emp，如果员工没有领导也需要查询出来（外连接写法）  
select a.name '员工',b.name '领导' from emp a left join emp b on a.managerid = b.id;
```

### 5.6. 联合查询-union,union all
``对于联合查询，就是把多次查询的结果结合起来，然后成为一个新的结果集。
查询语法如下:
```SQL
select 字段1，字段2…… from 表A ……
union(all)
select 字段1，字段2…… from 表A ……
```
示例代码如下：
```SQL
-- 联合查询  
-- 条件：1、查询薪资小于5000的员工  
--      2、查询年龄大于50的员工  
select * from emp where salary < 5000  
union  
select * from emp where age > 50;
```
``注意事项：
``1、对于联合查询的表的列数要一致，且字段数量也需要一致。
``2、union关键字会将结果去重，union all则是将结果全部显示。
### 5.7. 子查询
#### 5.7.1. 概念
如下图:
![](Pasted%20image%2020231106155539.png)
#### 5.7.2. 标量子查询
``该查询模式代表查询返回的结果为单个值，其中该查询常用的操作符有 = > < >= <= <>(不等于)等，适合查询某个对象的单个数据。
示例代码如下：
```SQL
-- 1、查询"销售部"的所有员工信息  
select * from emp where emp.dept_id = (select dept.id from dept where dept.name = '销售部');  
  
-- 2、查询在"方东白"入职后的员工信息  
select * from emp where entrydate > (select entrydate from emp where name = '方东白');
```
#### 5.7.3. 列子查询
``该查询模式代表查询返回的结果为一列值（多行），其中该查询常用的操作符有 IN、NOT IN、ANY、SOME、ALL，适合查多个对象的单个数据。
操作符解释如图所示：
![](Pasted%20image%2020231106215427.png)
示例代码如下：
```SQL
-- 列子查询  
-- 1、查询"销售部"和"市场部"的所有员工信息  
select id from dept where name = '销售部' or name = '市场部';  
-- in的作用是集合里的内容只要存在，就会查询到  
select * from emp where dept_id in (select id from dept where name = '销售部' or name = '市场部');  
  
-- 2、查询比财务部所有人工资高的员工信息  
select id from dept where name = '财务部';  
select salary from emp where dept_id = (select id from dept where name = '财务部');  
select * from emp where salary > all (select salary from emp where dept_id = (select id from dept where name = '财务部') ) ;  
  
-- 3、查询比"研发部"任意一人工资高的员工  
select id from dept where name = '研发部';  
select salary from emp where dept_id = (select id from dept where name = '研发部');  
select * from emp where salary > any (select salary from emp where dept_id = (select id from dept where name = '研发部'));  
-- 关于any和all的详解见谷歌收藏夹
```
#### 5.7.4. 行子查询
``该查询模式代表查询返回的结果为一行（多列），其中该查询常用的操作符有 =、<>、IN、NOT IN，适合查一个对象的多个数据。
示例代码如下：
```SQL
-- 行子查询  
-- 查询薪资与领导和张无忌一样的员工 的信息  
select salary,managerid from emp where name = '张无忌';  
select * from emp where (salary,managerid) = (select salary,managerid from emp where name = '张无忌');
```
#### 5.7.5. 表子查询
``该查询模式代表查询返回的结果为多行多列的表，其查询结果经常作为临时表写在 from 后面与其他表一起查询。
示例代码如下：
```SQL
-- 表子查询  
-- 1、查询与"鹿杖客"，"宋远桥"的职位和薪资相同的员工信息  
select job,salary from emp where name = '鹿杖客' or name = '宋远桥';  
-- 将(job,salary)这组字段看为一个字段，表查询即退化为列查询  
select * from emp where (job,salary) in (select job,salary from emp where name = '鹿杖客' or name = '宋远桥');  
-- 2、查询入职日期是"2006-01-01"之后的员工信息，及其部门信息  
select * from emp where entrydate > "2006-01-01";  
select e.*,d.* from (select * from emp where entrydate > "2006-01-01") e left join dept d on e.dept_id = d.id;
```
## 6. 事务
### 6.1. 简介
事务是一系列操作的集合，是一个不可分割的工作单位。事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即``这些操作要么同时操作成功，要么同时操作失败。
### 6.2. 事务操作
``注：在MySQL中事务默认为自动提交。
操作指令如下:
```SQL
方式一：

start transaction; 或 begin; -- 1、开启事务

commit; -- 2、提交事务

rollback; -- 3、回滚事务

方式二：
select @@autocommit; -- 查询当前的事务提交状态，MySQL默认为1

set @@autocommit = 1; -- 如需设置为手动，将1改为0即可
```
示例代码如下:
```SQL
-- ---------------------------- 事务操作（张三给李四转账1000元） ------------------------------ 数据准备  
create table account(  
    id int auto_increment primary key comment '主键ID',  
    name varchar(10) comment '姓名',  
    money int comment '余额'  
) comment '账户表';  
insert into account(id, name, money) VALUES (null,'张三',2000),(null,'李四',2000);  
  
-- 恢复数据  
update account set money = 2000 where account.name = '张三' or account.name = '李四';  
  
-- ------------------方式一------------------  
  
-- MySQL默认自动提交事务  
select @@autocommit;  
-- 手动控制事务  
set @@autocommit = 1; -- 如需设置为手动，将1改为0即可  
  
-- 转账操作  
-- 1.查询张三余额  
select money from account where account.name = '张三';  
  
-- 2.张三转出1000  
update account set money = money - 1000 where account.name = '张三';  
  
-- 3.李四收入1000  
update account set money = money + 1000 where account.name = '李四';  
  
-- 提交事务  
commit;  
  
-- 回滚事务  
rollback ;  
  
-- ------------------方式二------------------  
  
start transaction ; -- 开启事务，运行该语句后，在没有运行回滚和提交命令前都属于手动控制事务  
  
-- 转账操作  
-- 1.查询张三余额  
select money from account where account.name = '张三';  
  
-- 2.张三转出1000  
update account set money = money - 1000 where account.name = '张三';  
  
-- 3.李四收入1000  
update account set money = money + 1000 where account.name = '李四';  
  
-- 提交事务  
commit; -- 运行后该事务结束  
  
-- 回滚事务  
rollback ; -- 当发生异常，数据库的数据未发生改变，若依然运行这一语句 则表示该事务的结束
```
### 6.3. 事务四大特性(ACID)
``注：面试常问
如下图所示：
![](Pasted%20image%2020231108222146.png)
### 6.4. 并发事务问题
``注：面试常问
如下图所示：
![](Pasted%20image%2020231108222956.png)

### 6.5. 事务隔离级别
``注：面试常问
如下图所示：
![](Pasted%20image%2020231108230402.png)
该节内容较为抽象，[详细讲解视频55](https://www.bilibili.com/video/BV1Kr4y1i7ru?p=55&vd_source=7664b55184fd63da03a03ef6c9be4310)

``注：到此MySQL基础篇结束，进阶篇（面试常问！）关乎于数据库优化，索引等等内容，根据方向选择是否应该继续学习。