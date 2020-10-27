### 登录

`mysql -h localhost -P 3306 -proot`

- -h，主机
- -P，端口
- -u，用户
- -p，密码，p 之后紧接着就是密码不能有空格

`mysql -u root -proot`

一般情况本地开发就用上面的就可以

### 基本操作

`select version()` 查看数据库版本

`show databases;` 查看数据库

`use test;` 切换数据库

`show tables;` 查看表

`show databases();` 查看所处的库名

可以在 test 库查看其他库，`show tables from otherdatabase;`，这样的话还是在 test 库，只是查看了其他库的信息

### 语法规范

1. 不区分大小写，建议关键字大写，表名和列名小写

2. 每条查询语句最好用分号结尾

3. 每个查询语句都可以进行缩进和换行

4. 注释：

```
单行注释：#注释内容
单行注释：-- 注释内容
多行注释：/* 注释内容 */
```

### 加号

1. 字段都是数值类型，就是累加
2. 字段是字符型数字，则会将其转换成数值类型，转换失败则为 0
3. 字段只要有一个为 null，则结果就是 null
4. concat() 可以帮助字段连接

### IFNULL

判断是否为空，IFNULL(manager_id,'空')，manager_id 如果为空，那么显示空

### 条件运算符

1. \> 大于
2. < 小于
3. <> 不等于，!= 同样适用

### 逻辑运算符

1. and，&& 同样适用
2. or，|| 同样适用
3. not，| 同样适用

### 模糊查询

1. like

- % 代表任意多个字符，包括 0 个字符
- \_ 代表任意单个字符

2. between and

- 效果同 100<=x<=120，包含临界值

- 不在某个范围 not between 100 and 120

3. in

- 判断字段的值是否在给定的列表之中

4. is null

- 判断字段是否为空，字段名=null 无法适用

5. is not null

- 判断字段是否不为空

### 排序

order by 字段名 asc|desc

### 聚合函数

- sum、max、min、avg、count 都忽略 null 值

- sum(distince 字段名) 可以帮助先去重再运算

- 聚合函数与普通字段同时存在无意义，例如 select avg(age), name from users;

- 聚合函数可以与分组查询的字段进行搭配使用，例如 select avg(salary), job_id from job group by job_id;

### 分组查询

- 分组查询之后的过滤条件用关键字 having

- having 之后的过滤条件对应的字段都应该是使用了聚合函数的字段，若不是，那么就应该使用 where，而且是在 group by 之前

- 可以多个分组，用逗号隔开，例如，select avg(salary), dep_id, jib_id from user job group by dep_id,jib_id;

### 笛卡尔积

`select * from A,B`

最后结果是 A 表的每一行去关联 B 表的每一行，所以结果就是 A 表的 m 行与 B 表 n 行的乘积
