---
Title: Avoid SELECT *
Tip-number: 2
Tip-username: Vijayanand
Tip-username-profile: https://github.com/vijayanandp
Tip-description: Avoid SELECT *
---

If more data is read from the tables, the slower the query will become. It increases the time it takes for the disk operations. Also when the database server is separate from the web server, you will have longer network delays due to the data having to be transferred between the servers.

It is a good habit to always specify which columns you need when you are doing your SELECT's.
```php
// not preferred
$r = mysql_query("SELECT * FROM user WHERE user_id = 1");
$d = mysql_fetch_assoc($r);
echo "Welcome {$d['username']}";
 
// better:
$r = mysql_query("SELECT username FROM user WHERE user_id = 1");
$d = mysql_fetch_assoc($r);
echo "Welcome {$d['username']}";
 
// the differences are more significant with bigger result sets
```
