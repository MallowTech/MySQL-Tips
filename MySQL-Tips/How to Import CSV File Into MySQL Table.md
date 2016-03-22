---
title: How to Import CSV File Into MySQL Table
tip-number: 1
tip-username: Vijayanand
tip-username-profile: https://github.com/vijayanandp
tip-description: Import CSV File Into MySQL Table.
---

We often come across situation in which we need to import csv file to our MySQL Database. This tip is created to help you import CSV file into MySQL Table. We will use **LOAD DATA INFILE** statement to import CSV file into MySQL table. 

**Step 1:** Create a database table to which we need to import the data from file.

```php
CREATE TABLE products ( 
id INT NOT NULL AUTO_INCREMENT, 
name VARCHAR(255 NOT NULL,
quantity int(10) NULL, 
expiry_date DATE NOT NULL, 
amount DECIMAL(10 , 2 ) NULL, 
PRIMARY KEY (id) );
```


**Step 2:** Create a CSV file with the same number of columns and data type as in the table which we created above.


**Step 3:** We need a MySQL account which has FILE and INSERT privileges to that table.  

**Step 4:** Place the File in a path say /users/vijayanand/desktop/products.csv

**Step 5:** MySQL Query to load Data 
	
```php
LOAD DATA INFILE '/users/vijayanand/desktop/products.csv' 
INTO TABLE discounts 
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```
the fields in the file is terminated by a comma indicated by **FIELD TERMINATED BY ‘,'** and enclose by a double quotation mark specified by **ENCLOSED BY ‘"'** and each line of the CSV file is terminated by a newline character indicated by **LINES TERMINATED BY ‘\n'** .

The first line of our CSV file contains column heading we need to ignore this by specifying **IGNORE 1 ROWS**.

**Step 6:** We can cross check if the products table has been imported by using the query

```php
SELECT * FROM products;
```


**Note :** Sometimes the format of the data does not match the target columns in the table. In simple cases, you can transform it by using the SET clause in the  LOAD DATA INFILE statement.

Suppose the expiry date column in the  products.csv file is in  mm/dd/yyyy format.


When importing data into the products table, we have to transform it into MySQL date format by **using str_to_date()**

```php
LOAD DATA INFILE '/users/vijayanand/desktop/products.csv'
INTO TABLE products
FIELDS TERMINATED BY ',' ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS
(title,@expired_date,amount)
SET expired_date = STR_TO_DATE(@expired_date, ‘%m/%d/%Y');
```
