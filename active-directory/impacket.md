# Impacket

### Impacket MSSQL

Connect to MSSQL database with a domain account (windows auth)

```bash
impacket-mssqlclient oscp.exam/celia.almeda@10.10.182.142 -hashes :e728ecbadfb02f51ce8eed753f3ff3fd -windows-auth
```

**Database Exploration**

```
# We have selected a database and we list the tables
SQL (appdev  appdev@financial_planner)> SELECT table_name FROM information_schema.tables;

# Print all columns for a specific table in the database
SELECT column_name FROM information_schema.columns WHERE table_name = 'users';

# Print specific columns from a table
SELECT username,email,password_hash FROM users;
```
