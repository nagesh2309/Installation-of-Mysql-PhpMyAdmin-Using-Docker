# 🚀 MySQL & phpMyAdmin Setup Using Docker

This repository provides a quick and easy way to run MySQL and phpMyAdmin using Docker. It also includes steps to manage MySQL users and perform database import/export operations.

---

## 📦 Prerequisites

Make sure Docker is installed on your system:

```bash
sudo apt install docker.io
```

Install & Start MySQL Container (will run the container when system boots up)
```bash
sudo docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=mypass123 -d --restart always mysql
```

Install & Start PhpMyAdmin Container (will run the container when system boots up)
```bash
sudo docker run --name phpmyadmin -d --link mysql:db -p 8081:80 --restart always phpmyadmin/phpmyadmin
```

Managing MySQL Users
Access the MySQL CLI

```bash
sudo docker exec -it mysql bash
mysql -u root -p mypass123
```

Creating a New User and Grant Privileges (if required)

```bash
CREATE USER 'user1'@'%' IDENTIFIED BY 'user1@123';
GRANT ALL PRIVILEGES ON *.* TO 'user1'@'%';
FLUSH PRIVILEGES;
```

 Exporting a MySQL Database

 ```bash
sudo docker exec mysql mysqldump -u user1 -p"user1@123" test > test.sql
```

Importing a MySQL Database

```bash
docker exec -i mysql mysql -uuser1 -p'user1@123' <<<"CREATE DATABASE IF NOT EXISTS test;"
docker exec -i mysql mysql -uuser1 -p'user1@123' test < test.sql
```
