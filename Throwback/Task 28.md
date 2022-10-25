# We gotta drop the Load!

Now that we have a foothold onto the timekeep server we can being to enumerate what information we can find from the server. We can assume it is running a sql database somewhere because it had a login page. We also can assume that the web server is using xampp from the C:\ folder within the local disk. With this information we can easily find where the sql database is stored and how we can access it.


### DIY task -  Learn to enumerate SQL database 


Some Useful SQL queries for the tasks
```sql
# 1. Show all the databases after logging into the SQL database as root
show databases;

# 2. Enter into the database to further show all tables
use database;

# 3. Select all rows from database
select * from table1;

# 4. Show all tables in a database
show tables;

```


## Questions

1. What database are the timekeep login users located?
`timekeepusers`

2. What database are the domain users located in?
`domain_users`

3. What table was located in the domain users database?
`users`

4. What is the first username in the table?
`ClemonsD`

5. Submit flags for THROWBACK-TIME in Task 4.
`Answered!`

