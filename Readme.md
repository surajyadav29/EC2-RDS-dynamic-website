# Project Title: Dynamic Website Deployment using EC2 + RDS + Docker


# Description

Deployed a containerized Node.js application on AWS EC2 and connected it to AWS RDS (MySQL) for storing user data.
In this project, my focus was on deployment and infrastructure. I used a pre-built Docker image and deployed it on AWS EC2, then connected it to RDS. I worked on configuring environment variables, container networking, and database connectivity. I can also explain the application flow and queries used.

# Architecture

EC2 (Docker Node App) → RDS (MySQL)

# Technologies Used
AWS EC2
AWS RDS (MySQL)
Docker
Linux (Amazon Linux 2023)

# Steps Performed
1. Launch EC2 Instance
2. Install Docker
3. Run Application Container
4. Connect to RDS Database
5. Verify Data using MySQL Client


# Steps 1 
Created RDS database

# Step 2 
Launch EC2
Edit Security group Inbound rule HTTP on port 80, Sourse Anywhere-IPv4

# Step 3 
EC2 Instance Connect 
1. Update System
sudo yum update

2. Install Docker
sudo yum -y install docker

3. Start Docker Service
sudo systemctl start docker

4. Check Docker Status
sudo systemctl status docker

5. Pull Node + MySQL App Image
sudo docker pull philippaul/node-mysql-app:02

6. Run Application Container
sudo docker run --rm -p 80:3000 \
-e DB_HOST="database-1.cluem2sku8ih.eu-north-1.rds.amazonaws.com" 
-e DB_USER="admin" 
-e DB_PASSWORD="aaaaaaaa" 
-d philippaul/node-mysql-app:02

This means:
Port 80 (EC2) → 3000 (container)
Connected to RDS database

7. Run MySQL Client Container
sudo docker run -it --rm mysql:8.0
mysql -h database-1.cluem2sku8ih.eu-north-1.rds.amazonaws.com 
-u admin -p

Then enter password when prompted
Enter Password: aaaaaaaa

8. App is accessible via:

http://<EC2-Public-IP>

9. If want to run MySQL Queries
   
a. Show all databases
show databases;

b. Use your database
use my_app_db;

c. Show tables
show tables;

d. View data in table
select * from contacts;

Output:
+----+------------------------+
| id | username               |
+----+------------------------+
|  4 | yadavajay0505@gmal.com |
|  5 | ajay0505@gmal.com      |
+----+------------------------+

e. After adding new user data from browser 
View data in table
select * from contacts;

Output:
+----+------------------------+
| id | username               |
+----+------------------------+
|  4 | yadavajay0505@gmal.com |
|  5 | ajay0505@gmal.com      |
+----+------------------------+




