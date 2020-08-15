---
template: post
title: Login and Signup APIs developed using Spring Boot from scratch Part-I
slug: login-and-signup-api-developed-using-spring-boot-from-scratch-part-1
draft: false
date: 2020-08-13T16:35:58.403Z
description: >
  In this Part-I of the series you will learn to setup Spring Boot Environment
  and create your

  first project.
category: Spring Boot
tags:
  - spring
  - spring-framework
  - spring-boot
  - mysql
  - Eclipse
  - maven
  - Java
---
For Spring Boot Application Development I am using Lubuntu (a lightweight Linux distribution based on Ubuntu). You can use any platform of your choice (Windows, or MAC).

## **Requirements for Development:**

1. Java Installation (I will show you Installation of both Java 8 and Java 11).
2. Maven dependency manager Installation required by Spring Boot.
3. MySQL Installation.
4. IDE for development ([Eclipse](https://www.eclipse.org/downloads/) or [IntelliJ](https://www.jetbrains.com/idea/)).
5. Postman Installation (For testing Web service).

![Spring Initializr](/media/spring_init.jpg "Spring Boot Project Setup")

## Java Installation

Follow the following steps to still Java on your Linux Machine. I am using [OpenJDK](https://openjdk.java.net/).

Open your terminal and type the following command to install Java 8.

```shell
sudo apt install openjdk-8-jdk
// to check the java version

java -version
```

Open your terminal and type the following command to install Java 11. You can install any version of your choice. In this series I am using Java 8.

```shell
sudo apt install openjdk-11-jre-headless
// to check the java version

java -version
```

## Apache Maven

It is a powerful tool for project management that is based on POM (project object model). It is used by Spring For project build, dependency and documentation.

Open your terminal and type the following command to install [Maven](https://maven.apache.org/).

```shell
sudo apt install maven
// to check the maven version

mvn --version
```

## MySQL Installation and Setup

Open your terminal and type the following command to install [MySQL](https://www.mysql.com/).

```shell
sudo apt-get install mysql-server
// to check the mysql version

mysql --version
```

After installation is complete check if MySQL is running or not. Following command check the status of mysql service.

```shell
sudo systemctl status mysql.service
// to start the service type

sudo systemctl start mysql.service
// to stop the service type

sudo systemctl stop mysql.service
```

Its a good practice to secure the MySQL server. Type the following command and when asked for yes or no press Y for all.

```shell
sudo mysql_secure_installation
```

Login to MySQL Server

```shell
sudo mysql -u root -p
```

List Databases

```shell
show databases;
```

Create a Database

```shell
create database DataLoginSystem;
```

![MySQL Command Line Window](/media/mysql-2.jpg "MySQL Command Line Window")

Now we will create a new user which will have access only to our created database (DataLoginSystem).

```shell
CREATE USER 'userlogin'@'localhost' IDENTIFIED BY 'PassWord@12345';
```

To give all permission on our database (DataLoginSystem) to new user (userlogin) we need to first select our database then we will give permission.

```shell
use DataLoginSystem;
GRANT ALL PRIVILEGES ON DataLoginSystem TO 'userlogin'@'localhost';
```

Always be sure to reload all the privileges.

```shell
FLUSH PRIVILEGES;
```

To check if everything is working type the following commands.

```shell
sudo mysql -u userlogin -p
show databases;
```

![MySQL Command Line Window with New User Permission](/media/mysql-3.jpg "MySQL Command Line Window with New User Permission")

We are all set with our database setup.

## IDE for Development

For Eclipse

* Go to [Eclipse](https://www.eclipse.org/downloads/) download page and download the setup file.
* Extract the downloaded file.
* Goto extract folder and run the installer
* Follow the steps to install Eclipse.

We need to install Spring Tool Suite 4 inorder to work best with Spring Boot.
* For this install the tool through Marketplace under Help tab in Eclipse.

Video Link:- 
