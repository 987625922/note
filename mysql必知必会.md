MYSQL

1. select

   - 子查询

     作为子查询的SELECT语句只能在查询单个列，并且过多的子查询会影响性能

     ```mysql
     SELECT cust_name.cust_contect FROM custoners WHERE cust_id IN (SELECT cust_id FROM Orders WHERE order_num IN (SELECT Order_num FROM OrderItems WHERE prod_id = 1))
     ```

     作为计算字段使用的子查询

     ```mysql
     SELECT cust_name,(SELECT count(*) FROM Orders WHERE Order.id = Customers.id) AS orders FROM Customers ORDER BY cust_name
     ```

   - 联结表

     1. 笛卡尔积：由没有联结条件（即WHERE)的表关系返回的结果为笛卡尔积，检索出的行数是第一个表的行数乘以第二个表的行数

        SQL对一条SELECT语句中可以联结的表的数目没有限制，联结越多的表越耗费性能

        ```mysql
        SELECT vend_name,prod_name,prod_price FROM Venders,Produces WHERE Vendors.vend_id = Products.vend_id
        ```

     2. 内部联结（INNER JOIN 联结表名 ON 限定条件）

        ```mysql
        SELECT vend_name,prod_name,prod_price FROM Vendors INNER JOIN Produces ON vendors.id = Prodeucets.vend_id
        ```

     3. 外部联结

        联结一个表的行与另一个表的行，有时需要包含没有关联的行

        RICHT指出是OUTER JOIN右边的表，而LEFT指出是OUTER JOIN左边的表

        ```mysql
        SELECT Customers.cust_id,Orders.orser_num FROM Customers LEFT OUTER JOIN Orders ON Customers.cust_id = Orders.cust_id
        ```

   - 组合查询（UNION）

     ```mysql
     SELECT cust_name FROM Customers WHERE Cust_state IN ('IL','IN') OR cust_name = 'FUN'
     ```

2. 数据库表

   - 创建表

     ```
     CREATE TABLE Order(
     	order-num INTEGER NOT NULL PRIMARY KEY AUTO_INCREMENT,
     	quantity INTEGER DEFAULT
     );
     ```

   - 更新表

     1. 添加：ALTER TABLE Vendors ADD vend_phone CHAR(20)
     2. 删除：ALTER TABLE Vendors DROP COLUMN Vend_phone
     3. 删除表：DROP TABLE CustCopy

3. 约束

   - 主键

     1. 值不能重复且不能为空
     2. 主键值不能修改
     3. 行被删除后，其主键值不能分配到新行

   - 外键

     外键是表中的一个列，其值必须在另一个表的主键中列出

     ```mysql
     CREATE TABLE Orders(
     	order_num INTEGER PRIMAPY KEY,
         cust_id CHAR(10) NOT NULL REFEREBCES Customers(cust_id)
     )
     ```

   - 唯一约束

     唯一约束用来保证一个列中的数据唯一，类似于主键。区别：

     1. 表可以包含多个唯一约束，但主键只允许一个

     2. 唯一约束可包含NULL值

     3. 唯一约束可修改

     4. 列删除之后，唯一约束的值可在其他地方使用

     5. 唯一约束不能定义外键

        ```mysql
         CREATE TABLE tb_dept(
             id INT(11) PRIMARY KEY,
             name VARCHAR(22) UNIQUE,
             location VARCHAR(50)
             );
        ```

4. 索引

   索引用来排序数据以加快搜索和排序操作的速度

   ```
   CREATE INDEX prod_name_ind ON PRODUCTS(prod_name)
   ```

   prod_name_ind：索引名

   PRODUCTS：表名

   prod_name：表中的列名

5. SQL数据类型

   | 数值类型  |       |
   | --------- | ----- |
   | TINYINT   | 1字节 |
   | SMALLINT  | 2字节 |
   | MEDIUMINT | 3字节 |
   | INT       | 4字节 |
   | BIGINT    | 8字节 |
   | FLOAT     | 4字节 |
   | DOUBLE    | 8字节 |
   | DECIMAL   |       |

   --

   | 字符串类型 |                  |            |
   | ---------- | ---------------- | ---------- |
   | CHAR       | 0-255字节        | 定长字符串 |
   | VARCHAR    | 0-65535字节      | 变长字符串 |
   | TINYBLOB   | 0-255字节        | ?          |
   | TINYTEXT   | 0-255字节        | ?          |
   | BLOB       | 0-65535字节      |            |
   | TEXT       | 0-65525字节      |            |
   | MEDIUMBLOB | 0-16777215字节   |            |
   | MEDIUMTEXT | 0-16777215字节   |            |
   | LONGBLOB   | 0-4294967295字节 |            |
   | LONGTEXT   | 0-429496729字节  |            |

   

