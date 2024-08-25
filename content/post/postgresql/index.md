---
title: "Postgresql"
description: 
date: 2024-05-06T22:48:30+08:00
image: 
math: 
license: 
hidden: false
comments: true
draft: true
---

```sql
-- login
plsql -Uusername -h127.0.0.1 -p5432
psql (12.18 (Debian 12.18-1.pgdg120+2))
Type "help" for help.

-- create database
root=# CREATE DATABASE test;
CREATE DATABASE

-- connect table to test
root=# \c test;
You are now connected to database "test" as user "root".

-- create table test
test=# CREATE TABLE test (
test(# id BIGSERIAL NOT NULL PRIMARY KEY,
test(# first_name VARCHAR(50) NOT NULL,
test(# last_name VARCHAR(50) NOT NULL,
test(# gender VARCHAR(7) NOT NULL,
test(# date_of_birth DATE NOT NULL,
test(# email VARCHAR(128) );
CREATE TABLE

-- display table info of test 
test=# \d test;
                                       Table "public.test"
    Column     |          Type          | Collation | Nullable |             Default              
---------------+------------------------+-----------+----------+----------------------------------
 id            | bigint                 |           | not null | nextval('test_id_seq'::regclass)
 first_name    | character varying(50)  |           | not null | 
 last_name     | character varying(50)  |           | not null | 
 gender        | character varying(7)   |           | not null | 
 date_of_birth | date                   |           | not null | 
 email         | character varying(128) |           |          | 
Indexes:
    "test_pkey" PRIMARY KEY, btree (id)

-- drop table test
test=# DROP TABLE test;
DROP TABLE

-- create table person
test=# CREATE TABLE person (
id BIGSERIAL NOT NULL PRIMARY KEY,
first_name VARCHAR(50) NOT NULL,
last_name VARCHAR(50) NOT NULL,
gender VARCHAR(7) NOT NULL,
date_of_birth DATE NOT NULL,
email VARCHAR(128) );
CREATE TABLE

-- display table info of person
test=# \d person
                                       Table "public.person"
    Column     |          Type          | Collation | Nullable |              Default               
---------------+------------------------+-----------+----------+------------------------------------
 id            | bigint                 |           | not null | nextval('person_id_seq'::regclass)
 first_name    | character varying(50)  |           | not null | 
 last_name     | character varying(50)  |           | not null | 
 gender        | character varying(7)   |           | not null | 
 date_of_birth | date                   |           | not null | 
 email         | character varying(128) |           |          | 
Indexes:
    "person_pkey" PRIMARY KEY, btree (id)

-- display table list
test=# \d
             List of relations
 Schema |     Name      |   Type   | Owner 
--------+---------------+----------+-------
 public | person        | table    | root
 public | person_id_seq | sequence | root
(2 rows)

test=# 

test=# select * from person offset 5 fetch first 5 row only;
test=# select * from person offset 5 limit 5;


```
