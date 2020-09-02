---
template: post
title: Login and Signup APIs developed using Spring Boot from scratch Part-II
slug: login-and-signup-api-developed-using-spring-boot-from-scratch-part-2
draft: false
date: 2020-08-15T09:17:50.556Z
description: In this Part-II of the series you will learn to configure our
  database setting, create models and repositories.
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
Open the terminal and type the following commands.

```shell
$ cd Downloads
$ unzip loginsignup.zip
```

![Unzip project](/media/unzip_project.jpg "Unzip project")

Now open intelliJ or Eclipse to import the project.

![Import Project](/media/open.jpg "Import Project")

Wait for some time to finish the import. Project Structure at start:- 

![Project Structure Start](/media/initail-project-structure.jpg "Project Structure Start")

## Creating models

![Directory Structure After creating models](/media/models.jpg "Directory Structure After creating models")

* Create a package under loginsignup with name **models.**
* Create two **class Usermodel** & Roles and a **enum RoleType.**

  ### Usermodel

  ```java
  package com.loginsignup.models;
  import java.util.HashSet;
  import java.util.Set;
  import javax.persistence.Entity;
  import javax.persistence.FetchType;
  import javax.persistence.GeneratedValue;
  import javax.persistence.GenerationType;
  import javax.persistence.Id;
  import javax.persistence.JoinColumn;
  import javax.persistence.JoinTable;
  import javax.persistence.ManyToMany;
  import javax.persistence.Table;
  import javax.persistence.UniqueConstraint;
  import javax.validation.constraints.Email;
  import javax.validation.constraints.NotBlank;
  import javax.validation.constraints.Size;
  import com.loginsignup.util.CustomTimeStamp;
  import org.hibernate.annotations.NaturalId;
  @Entity
  @Table(name = "users", uniqueConstraints = { @UniqueConstraint(columnNames = { "username" }),
          @UniqueConstraint(columnNames = { "emailId" }) })
  public class Usermodel extends CustomTimeStamp {
      /**
       *
       */
      private static final long serialVersionUID = 1L;
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      @Size(max = 20)
      @NotBlank
      private String name;
      @Size(max = 20)
      @NotBlank
      private String username;
      @NotBlank
      @Size(max = 70)
      @NaturalId
      @Email
      private String emailId;
      @NotBlank
      @Size(max = 100)
      private String password;
      public Long getId() {
          return id;
      }
      public void setId(Long id) {
          this.id = id;
      }
      public String getName() {
          return name;
      }
      public void setName(String name) {
          this.name = name;
      }
      public String getUsername() {
          return username;
      }
      public void setUsername(String username) {
          this.username = username;
      }
      public String getEmailId() {
          return emailId;
      }
      public void setEmailId(String emailId) {
          this.emailId = emailId;
      }
      public String getPassword() {
          return password;
      }
      public void setPassword(String password) {
          this.password = password;
      }
      public Usermodel(String name, String username, String emailId, String password) {
          this.name = name;
          this.username = username;
          this.emailId = emailId;
          this.password = password;
      }
      public Usermodel() {
      }
      @ManyToMany(fetch = FetchType.LAZY)
      @JoinTable(name = "user_roles", joinColumns = @JoinColumn(name = "user_id"), inverseJoinColumns = @JoinColumn(name = "role_id"))
      private Set<Roles> role = new HashSet<>();
      public Set<Roles> getRole() {
          return role;
      }
      public void setRole(Set<Roles> role) {
          this.role = role;
      }
  }
  ```

  ### Roles

  ```java
  package com.loginsignup.models;
  import javax.persistence.Column;
  import javax.persistence.Entity;
  import javax.persistence.EnumType;
  import javax.persistence.Enumerated;
  import javax.persistence.GeneratedValue;
  import javax.persistence.GenerationType;
  import javax.persistence.Id;
  import javax.persistence.Table;
  import org.hibernate.annotations.NaturalId;
  @Entity
  @Table(name = "roles")
  public class Roles {
      // property of Roles class Id, RoleType
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      @Enumerated(EnumType.STRING)
      @NaturalId
      @Column(length = 70)
      private RoleType name;
      // Default Constractor
      public Roles() {
      }
      public Roles(RoleType name) {
          this.name = name;
      }
      public Long getId() {
          return id;
      }
      public void setId(Long id) {
          this.id = id;
      }
      public RoleType getName() {
          return name;
      }
      public void setName(RoleType name) {
          this.name = name;
      }
  }
  ```

  ### RoleType

  ```java
  package com.loginsignup.models;
  public enum RoleType {
      USER_ROLE, ADMIN_ROLE
  }
  ```

  ## Creating repository

  ![Directory Structure After creating repository](/media/repository.jpg "Directory Structure After creating models")

  ### UserRepository

  ```java
  package com.loginsignup.repository;
  import java.util.List;
  import java.util.Optional;
  import com.loginsignup.models.Usermodel;
  import org.springframework.data.jpa.repository.JpaRepository;
  import org.springframework.stereotype.Repository;
  @Repository
  public interface UserRepository extends JpaRepository<Usermodel, Long> {
      Optional<Usermodel> findByUsername(String username);
      boolean existsUsermodelByUsername(String username);
      boolean existsUsermodelByEmailId(String emailId);
  }
  ```

  ### UserRoleRepository

  ```java
  package com.loginsignup.repository;
  import java.util.Optional;
  import com.loginsignup.models.RoleType;
  import com.loginsignup.models.Roles;
  import org.springframework.data.jpa.repository.JpaRepository;
  import org.springframework.stereotype.Repository;
  @Repository
  public interface UserRoleRepository extends JpaRepository<Roles, Long> {
      Optional<Roles> findByName(RoleType name);
  }
  ```

  ## Database Configuration

  ```java
  spring.datasource.driverClassName = com.mysql.cj.jdbc.Driver
  spring.datasource.url= jdbc:mysql://localhost:3306/DataLoginSystem?serverTimezone=UTC&useLegacyDatetimeCode=false
  spring.datasource.username=userlogin
  spring.datasource.password=PassWord@12345

  spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.MySQL5InnoDBDialect

  spring.jpa.hibernate.ddl-auto=update
  spring.jpa.show-sql=true
  ```

  **To be Continue.......**