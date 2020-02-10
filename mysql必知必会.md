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
     	order-num INTEGER NOT NULL AUTO_INCREMENT,
     	quantity INTEGER DEFAULT
     );
     ```

   - 更新表

     1. 添加：ALTER TABLE Vendors ADD vend_phone CHAR(20)
     2. 删除：ALTER TABLE Vendors DROP COLUMN Vend_phone
     3. 删除表：DROP TABLE CustCopy

3. 约束