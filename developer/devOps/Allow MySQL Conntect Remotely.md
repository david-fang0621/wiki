1. AWS EC2 Instance → Security Groups → In Bounce Rules → MySQL/Aurora (Port 3306)
2. Connect to EC2 instance using SSH
3. Open `mysqld.cnf` file

```bash
sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf
```

1. Change bind-address from 127.0.0.1 to 0.0.0.0
2. Create MySQL user

```sql
CREATE USER 'username'@'%' IDENTIFIED BY 'password';
GRANT PRIVILEGE on *.* TO 'username'@'%' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```
