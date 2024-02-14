Step:1 (clone git repo.)
`git clone https://github.com/LondheShubham153/two-tier-flask-app.git`

Step:2 (go inside clone repo.)
`cd two-tier-flask-app/`

Step:3 (build docker file and create images)
`docker build -t flask-app .`

Step:4 (Create network)
`docker network create two-tire-app-nw`

Step:5 (create mysql container)
`docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=test@123 -e MYSQL_DATABASE=testdb -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin --name mysql --network two-tire-app-nw mysql:latest`

Step:6 (check running container of mysql)
`docker ps`

Step:7 (go inside mysql container)
`docker exec -it <container ID> bash`

Step:8 (go inside mysql as a root user and enter password)
`mysql -u root -p
Enter password: test@123`

Step:9 (give all privileges to admin user)
`mysql> GRANT ALL PRIVILEGES ON default_db.* TO 'admin'@'%';`

Step:10 (remove all privilege)
`mysql> FLUSH PRIVILEGES;`

Step:11 (create database)
`mysql> CREATE DATABASE default_db;`

Step:12 (show database)
`mysql> SHOW DATABASES;`

Step:13 (for use databse)
`mysql> use default_db;`

Step:14 (create table inside database)
`CREATE TABLE messages (id INT AUTO_INCREMENT PRIMARY KEY,message TEXT);`

Step:15 (create python django container using mysql credential)
`docker run -d -p 5000:5000 -e MYSQL_HOST=mysql -e MYSQL_DATABASE=testdb -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin --name flask-container4 --network two-tire-app-nw flask-app:latest`

Step:16 (check in localhost)
`http://localhost:5000/`
