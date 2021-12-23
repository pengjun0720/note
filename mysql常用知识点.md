# mysql常用知识点
## 修改表结构
### 在某个字段之后添加表字段  默认值 注释
ALTER TABLE goods_goods ADD isTrainCourse INT ( 1 ) DEFAULT 0 COMMENT '是否是实训课程 (0: 不是, 1: 是)' AFTER isExam;
## 常用mysql函数
### CONCAT_WS(separator,str1,str2,…)函数
SELECT CONCAT_WS(',','First name',NULL,'Last Name');返回结果为
First name,Last Name
### IF(expr1,expr2,expr3)函数
IF("document"!=ttcl.train_lesson_object_type, "", ttcl.train_course_chapter_id)
### Mysql字符串字段判断是否包含某个字符串的方法
- **like**

```mysql
SELECT * FROM 表名 WHERE 字段名 like "%字符%";
```

- **find_in_set()**

```mysql
SELECT * FROM users WHERE find_in_set('字符', 字段名);
```

- **locate(字符,字段名)**

使用locate(字符,字段名)函数，如果包含，返回>0的数，否则返回0 

position in

```mysql
select * from 表名 where locate(字符,字段)
select * from 表名 where position(字符 in 字段);
```

- **INSTR(字段,字符)**

```mysql
select * from 表名 where INSTR(字段,字符)
```

### Mysql 判空操作

#### 1、isnull(expr)

```mysql
-- 如果expr为null，则返回1，否则返回0
SELECT '' IS NULL;  -- 0
SELECT null IS NULL;  -- 1
SELECT NULL IS NOT NULL;  -- 0
SELECT '' IS NOT NULL;  -- 1
SELECT ISNULL('');  -- 0
SELECT ISNULL(1/0);  -- 1
SELECT ISNULL(1/NULL);  -- 1
SELECT ISNULL(NULL);  -- 1
```

#### 2、ifnull(expr1, expr2)

```mysql
-- expr1不为null的情况下，返回expr1，返回expr2
SELECT IFNULL(1,2) from dual; -- 1
SELECT IFNULL(null,2) from dual; -- 2
SELECT IFNULL(1/0,'can not be null') from dual; -- 'can not be null'
```

#### 3、nullif(expr1, expr2)

```mysql
-- 如果两个表达式相同，则返回null，否则返回expr1的值 个人感觉应该叫null if equals
SELECT NULLIF(1,3) from dual; -- 1
SELECT NULLIF(3,3) from dual; -- null
SELECT NULLIF(1+2,3) from dual; -- null
```

#### 4、coalesce(expr1, expr2,... exprN)

```mysql
-- 返回第一个不是null的值
SELECT COALESCE(null,1/0,2) from dual; -- 2
SELECT COALESCE(null,1/0,2,3) from dual; -- 2
-- 两个参数的情况下，相当于ifnull
SELECT IFNULL(null,2) from dual; -- 2
SELECT COALESCE(null,2) from dual; -- 2
```

#### 5、关于日期的函数

```mysql
SELECT CURDATE();
SELECT DATE(create_time) FROM table_name WHERE id =value;
```

