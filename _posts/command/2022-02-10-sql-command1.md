---
layout: post
current: post
cover:  assets/built/images/mysql.png
navigation: True
title: SQL 명령어
date: 2022-02-10 10:00:00
tags: [command]
class: post-template
subclass: 'post'
author: In8989
---

### SQL 자주쓰는 명령어

* DB 접속
~~~ mysql
mysql -u {계정ID} -p;
mysql -u {계정ID} -p {DB 이름};
mysql -u {계정ID} -p {계정PW};
mysql -u {계정ID} -p {계정PW} {DB 이름};
~~~

* CREATE ( DB, TABLE 생성)
~~~ mysql
CREATE DATABASE {테이블명} CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
CREATE TABLE {테이블명} 
(
    {칼럼명1} {데이터타입1}
    {칼럼명2} {데이터타입2}
    …
);
~~~

* USE
~~~ mysql
USE {테이블명};
~~~

* DROP
~~~ mysql
DROP DATABASE {테이블명};
~~~

* ALTER (추가, 수정, 삭제)
~~~ mysql
ALTER TABLE {테이블명} ADD {컬럼명}{데이터타입};
ALTER TABLE {테이블명} MODIFY COLUMN {컬럼명}{데이터타입};
ALTER TABLE {테이블명} DROP {컬럼명};
~~~

* SELECT
~~~ mysql
SELECT * FROM {테이블명};
~~~

* INSERT
~~~ mysql
INSERT INTO {테이블명} VALUES ({값1}, {값2}, {값3}…);
INSERT INTO {테이블명}({필드이름1}{필드이름2}{필드이름3}) VALUES ({값1}, {값2}, {값3});
~~~

* UPDATE ( 안전을 위해 조건 필수 )
~~~ mysql
UPDATE {테이블명} SET {컬럼명}='값' WHERE {조건};
~~~

* DELETE ( 안전을 위해 조건 필수 )
~~~ mysql
DELETE FROM {테이블명} WHERE {조건};
~~~

* PK 초기화
~~~ mysql
ALTER TABLE {테이블명} AUTO_INCREMENT = 1;
~~~

* Join
~~~ mymysql
SELECT
{테이블명1}.{컬럼명1},
{테이블명2}.{컬럼명2}
FROM {테이블명1}
JOIN {테이블명2}
ON {테이블명1}.{컬럼명1} = {테이블명2}.{컬럼명2};
~~~
