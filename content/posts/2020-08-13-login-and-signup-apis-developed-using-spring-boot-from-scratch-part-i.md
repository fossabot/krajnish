---
template: post
title: Login and Signup APIs developed using Spring Boot from scratch Part-I
slug: login-and-signup-api-developed-using-spring-boot-from-scratch-part-1
draft: true
date: 2020-08-13T16:35:58.403Z
description: >
  In this Part-I of the series you will learn to setup Spring Boot Environment
  and create your

  first project.
category: Spring Boot
tags:
  - spring
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
```

Open your terminal and type the following command to install Java 11. You can install any version of your choice. In this series I am using Java 8.

```shell
sudo apt install openjdk-11-jre-headless
```

``