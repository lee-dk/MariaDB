# Maria DB

## 1. Maria DB 설치

>- Maria DB 다운로드 & 설치
>   - DB Platform : https://mariadb.com/downloads/
>- Maria DB 라이브러리 설치

## 2. 데이터 베이스 & 테이블 생성

> - 기본 데이터베이스 보기
>
>   ```mariadb
>   MariaDB [(none)]> show databases;
>   +--------------------+
>   | Database           |
>   +--------------------+
>   | information_schema |
>   | mysql              |
>   | performance_schema |
>   | test               |
>   +--------------------+
>   4 rows in set (0.009 sec)
>   ```
>
>   - 기본으로 만들어져있는 데이터 베이스들을 보여준다.
>
>     
>
> - 'test' 데이터베이스 사용
>
>   ```mariadb
>   MariaDB [(none)]> use test;
>   Database changed
>   MariaDB [(test)]> show databases;
>   +--------------------+
>   | Database           |
>   +--------------------+
>   | information_schema |
>   | mysql              |
>   | performance_schema |
>   | test               |
>   +--------------------+
>   4 rows in set (0.001 sec) 
>   ```
>
>   - `use (데이터베이스 명)` : 생성된 DB가 있다면 그 데이터베이스를 사용하겠다는 뜻
>
>     
>
> - 'work' 데이터베이스 생성
>
>   ```mariadb
>   MariaDB [test]> create database work;
>   Query OK, 1 row affected (0.002 sec)
>   
>   MariaDB [test]> show databases;
>   +--------------------+
>   | Database           |
>   +--------------------+
>   | information_schema |
>   | mysql              |
>   | performance_schema |
>   | test               |
>   | work               |
>   +--------------------+
>   5 rows in set (0.001 sec)
>   
>   MariaDB [test]> use work;
>   Database changed
>   ```
>
>   - `create database (데이터베이스 명)` : 새로운 데이터베이스 생성
>
>     
>
> - 'work'에 테이블 생성
>
>   ```mariadb
>   MariaDB [work]> create table goods (
>       -> code int primary key,
>       -> name varchar(20) not null,
>       -> su int,
>       -> dan int);
>   Query OK, 0 rows affected (0.038 sec)
>   ```
>   
>   - `create table (테이블 명) (사용할 인수들)` : 테이블을 만들 때 인수를 지정해줘야함
>
> - 테이블 목록 보기
>
>   ```mariadb
>   MariaDB [work]> show tables;
>   +----------------+
>   | Tables_in_work |
>   +----------------+
>   | goods          |
>   +----------------+
>   1 row in set (0.000 sec)
>   ```
>
>   - `show tables` : 지정된 DB안에 어떤 테이블이 있는지 보여준다
>
>     
>
> - 테이블에 레코드(내용) 추가
>
>   ```mariadb
>   MariaDB [work]> insert into goods values (1,'냉장고', 2, 850000);
>   Query OK, 1 row affected (0.012 sec)
>   
>   MariaDB [work]> insert into goods values (2,'세탁기', 3, 550000);
>   Query OK, 1 row affected (0.004 sec)
>   
>   MariaDB [work]> insert into goods values (3,'전자레인지', 2, 350000);
>   Query OK, 1 row affected (0.004 sec)
>   
>   MariaDB [work]> insert into goods values (4,'HDTV', 3, 1500000);
>   Query OK, 1 row affected (0.004 sec)
>   ```
>
>   - `insert into goods values (추가할 레코드1, 추가할 레코드2, ..)` : 레코드 추가
>
>     
>
> - 테이블에서 레코드 조회
>
>   ```mariadb
>   MariaDB [work]> select * from goods;
>   +------+------------+------+---------+
>   | code | name       | su   | dan     |
>   +------+------------+------+---------+
>   |    1 | 냉장고      |    2 |  850000 |
>   |    2 | 세탁기      |    3 |  550000 |
>   |    3 | 전자레인지   |    2 |  350000 |
>   |    4 | HDTV       |    3 | 1500000 |
>   +------+------------+------+---------+
>   4 rows in set (0.000 sec)
>   ```
>
>   - `select * from (테이블 명)` : 테이블에 추가된 레코드를 보여준다
>
>     
>
> - 사용자 계정만들고 권한 주기
>
>   ```mariadb
>   MariaDB [work]> create user 'scott'@'localhost' identified by 'tiger';
>   Query OK, 0 rows affected (0.003 sec)
>   
>   MariaDB [work]> grant all privileges on work.* to 'scott'@'localhost';
>   Query OK, 0 rows affected (0.003 sec)
>   
>   MariaDB [work]> flush privileges;
>   Query OK, 0 rows affected (0.001 sec)
>   
>   MariaDB [work]> quit
>   Bye
>   ```
>
>   - `create user '(계정)'@'localhost' identified by '(비밀번호)'` : 계정 생성
>   - `grant all privileges on work.* to '(계정)'@'localhost'` : ( * )모든 권한 부여
>   - `flush privileges` : grant 테이블을 reload함으로서 변경 사항을 즉시 반영
>   - `quit` : 작업 종료

