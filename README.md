# MariaDB

- MySql은 유료입니다
- MySql이 유료로 바뀌기 전에 git을 fork해서 만들어진 것이 MariaDB
- 문법이 99.9% 동일
- [설치](https://mariadb.org/download/?os=windows&cpu=x86_64&pkg=msi&mirror=blendbyte&t=mariadb&p=mariadb&r=11.7.2)

## 설치 시 주의 사항

- port 충돌 : 3308 번으로 변경(3306 - MySql용 포트 충돌)
- 비밀번호 : 1234
- 설치 중 한글 사용 체크
  - Use UTF8 as default character set and collation
  - 문자를 입력할때 한글 및 다양한 언어들이 정상적으로 입력되도록 하는 옵션

## Path 설정

- 하단의 윈도우 검색창에서 `환경 변수 편집` 검색
- `환경 변수` 버튼 클릭 > 하단의 `시스템 변수` > `Path` 항목 더블클릭으로 수정 진입
- `C:\Program Files\MariaDB 11.7\bin` 추가

## SQL 구문으로 스키마 즉 데이터베이스 생성하기

```sql
-- 데이터베이스 목록보기
show databases;

-- 데이터베이스 즉 스키마 만들기
create database board;

-- 데이터베이스 목록보기
show databases;
```

## SQL 구문으로 스키마(데이터베이스) 안에 Table 생성 및 컬럼명, 컬럼 속성 세팅하기

```sql
-- 스키마(데이터베이스)에 표를 생성한다
-- 어느 스키마를 쓸지 결정을 해주어야 한다
use board;
```

- author 테이블 생성

```sql
-- create table 테이블명
create table author(
	id int primary key, -- pk로 항목의 제약조건을 지정함
	name varchar(100),
	email varchar(30),
	password varchar(20)
);
```

- 실행된 sql 구문보기

```sql
-- 실행된 쿼리 다시보기
show create table author;
```

- 실행된 구문

```sql
CREATE TABLE `author` (
  `id` int(11) NOT NULL,
  `name` varchar(100) DEFAULT NULL,
  `email` varchar(30) DEFAULT NULL,
  `password` varchar(20) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci
```

- posts 테이블 생성

```sql
-- board 스키마(데이터베이스)에 posts 테이블 생성하기
create table posts(
	id int,
    title varchar(255),
    content varchar(3000),
    author_id int not null, -- FK
    primary key(id),
    foreign key(author_id) references author(id)
);
```

- 실행된 구문

```sql
CREATE TABLE `posts` (
  `id` int(11) NOT NULL,
  `title` varchar(255) DEFAULT NULL,
  `content` varchar(3000) DEFAULT NULL,
  `author_id` int(11) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `author_id` (`author_id`),
  CONSTRAINT `posts_ibfk_1` FOREIGN KEY (`author_id`) REFERENCES `author` (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_uca1400_ai_ci'
```

## 테이블 및 속성 변경 문법(ALTER)

- 테이블명 변경하기

```sql
use 스키마명;

use board; -- board 스키마 사용하겠다는 쿼리

alter table 테이블명 rename 새테이블명;

-- 테이블명 변경
alter table posts rename post;
-- 테이블 목록보기
show tables;

-- 테이블명 변경
alter table post rename posts;
-- 테이블 목록보기
show tables;
```

- 테이블에 컬럼 추가하기

```sql
alter table 테이블명 add column 데이터타입;

-- author 테이블에 age int 컬럼 추가하기
alter table author add column age int;

-- 상세 정보보기
describe author;
```

- 테이블에 있는 컬럼 삭제하기

```sql
alter table 테이블명 drop column 컬럼명;

-- author 테이블에 age 컬럼 삭제하기
alter table author drop column age;

-- 상세 정보보기
describe author;
```

- 컬럼명 변경하기

```sql
alter table 테이블명 change column 컬럼명 새컬럼명 데이터타입;

-- posts 테이블에 content를 contents로 변경
alter table posts change column content contents varchar(3000);

-- 상세 정보보기
describe posts;
```

- 특정 컬럼의 속성 변경하기

```sql
alter table 테이블명 modify column 컬럼명 데이터타입 제약조건;

-- author 테이블의 email 컬럼 변경하기
alter table author modify column email varchar(30) not null;

-- 상세 정보보기
describe author;

-- posts 테이블의 title 속성 변경
alter table posts modify column title varchar(255) not null;

-- 상세 정보보기
describe posts;
```

## 데이터 추가(INSERT)

- 테이블에 새로운 데이터(레코드) 추가

```sql
insert into 테이블명 (컬럼명, 컬럼명, ...) values (값, 값, ...);

-- 상세 정보보기
describe author;

-- 레코드 추가
insert into author (id, name, email, password) values (1, "홍길동", "hong@naver.com", "1234");

-- 레코드 내용 전체 출력
select * from author;

-- 상세 정보보기
describe posts;

-- author 테이블에 id가 존재하는 레코드를 posts에 추가
insert into posts (id, title, contents, author_id) values (1, "react", "react...", 1);

-- 레코드 내용 전체 출력
select * from posts;

-- author 테이블에 id가 존재하지 않는 경우 레코드를 posts에 추가
insert into posts (id, title, contents, author_id) values (2, "java", "java...", 2); -- 거부됨

-- 레코드 내용 전체 출력 (변화가 없다)
select * from posts;
```

## 데이터 수정(UPDATE)

```sql
-- 레코드 추가
insert into author (id, name, email, password) values (2, "홍길동2", "hong2@naver.com", "1234");
insert into author (id, name, email, password) values (3, "홍길동3", "hong3@naver.com", "1234");

-- 전체 데이터 출력
select * from author;
```

```sql
update 테이블명 set 컬럼명=값 where 조건;

-- Editor에서 Safe Update Mode가 Where절을 요구하도록 세팅 (SET SQL_SAFE_UPDATES = 0)
update author set email="a@a.net"; -- 실행안됨
update author set email="a@a.net" where id = 1; -- 실행

-- 전체 데이터 출력
select * from author;
```

## 데이터 삭제(DELETE)

- where 조건은 필수
- where가 없으면 모두 삭제됨

```sql
delete from 테이블명 where 조건;
delete from 테이블명 where 필드이름=값;

-- author에서 id가 2인 레코드 삭제
delete from author where id = 2;

-- 전체 데이터 출력
select * from author;
```

## 삭제에 관한 내용

- delete from 테이블명

  - 데이터는 지워지고 테이블 자체는 남아있다
  - 복구 가능

- truncate table 테이블명

  - 데이터를 지우고 테이블도 삭제한다
  - 복구 불가능

- drop table 테이블명
  - 데이터를 지우고 테이블도 삭제한다
  - 복구 불가능

## 데이터 조회(SELECT) 구문

- 개발자가 가장 많이 사용하는 구문
- 복잡한 옵션으로 값 추출

```sql
select * from 테이블명;

-- 전체 데이터 출력
select * from author;
```

```sql
select 컬럼, 컬럼
from 테이블명
where 조건;
```

```sql
-- 전체 데이터 출력
select * from author;

-- 컬럼별로 출력
select id, name from author;

-- where 조건으로 출력
select * from author where id = 1;
select email, name from author where id = 1;

-- 비교문 사용하기
select * from author where id > 1;
select * from author where id >= 1;

-- AND, OR 조건 사용하기
select * from author where id >= 1 and name = "홍길동2";
select * from author where id = 1 or name = "홍길동2";

-- 중복 값 제거
select distinct password from author;

-- 오름차순 정렬(기본)
select * from author order by id asc;
-- 내림차순 정렬
select * from author order by id desc;
select * from author order by email desc;

-- 개수제한 (2개만)
select * from author order by name limit 2;
```

## 컬럼 및 테이블에 별도의 이름 붙이기

- 컬럼명에 별칭 붙이기

```sql
select name as "이름", email as "메일주소" from author;
```

- 테이블명에 별칭 붙이기

```sql
select name as "이름", email as "메일주소" from author;
select name as "이름", email as "메일주소" from author as ttt;
select ttt.name, ttt.email from author as ttt;
```

- null을 조회조건으로 사용
  - null은 `값이 없다`는 말입니다
  - `is null`은 값이 없는 경우 검색
  - `is not null`은 값이 있는 경우 검색

## 데이터 종류

### 1. 정수

- tinyint : -128 ~ 127 까지 표현 가능, 나이 등을 표현할 때 사용
- int : -20억 ~ 20억 까지 표현 가능, 일반적 정수에 사용
- bigint : 가장 큰 범위, 글로벌 서비스 시 사용
- unsigned : 무조건 양수로 (tinyint unsigned : 0 ~ 255)

### 2. 실수 (소수점)

- decimal(진수, 소수점자리) : 증권, 금융거래 정보 등 정확한 정보가 필요할 때 사용
- float, double : 일반적인 실수

### 3. 문자

- char(길이)

  - 0 ~ 255 문자, 내용과 상관없이 `길이만큼 저장 공간을 차지`
  - 성별, 전화번호, 주민번호 등

- varchar(길이)

  - 0 ~ 65535 문자
  - 가장 많이 사용함
  - 가변 길이 : 내용만큼 저장 공간을 차지
  - 이름, 주소, 상품명 등

- text

  - 가변 길이
  - 별도로 길이 지정못함
  - varchar보다는 더 큰 범위 지정

- blob

  - 바이너리 데이터
  - 이미지 파일을 문자열로 전환 후 저장할 때(픽셀의 값 모두 글자로 저장)
  - 지금은 일반적으로 blob보다는 실제 파일을 서버에 저장

- enum
  - 미리 들어갈 수 있는 특정 데이터 목록 값을 지정
  - "admin", "member"등의 권한 설정 시 사용

### 4. 날짜 타입

- date
  - 날짜만 저장 (YYYY-MM-DD)
  - 생년월일에 사용
- datetime
  - 날짜와 시간까지 저장
  - 옵션을 주면 예를 들어 m 옵션을 주면 micro second 단위까지 저장
  - YYYY-MM-DD HH:MM:SS
  - 가장 많이 사용 (주문시간, 글 작성 시간 등)
  - 현재시간을 출력하는 함수 : current_timestamp(), now()
