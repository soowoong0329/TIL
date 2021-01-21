# SQL 기본

## `select문`

### `select from`

```mariadb
SELECT select_expr
    [FROM table_references]
    [WHERE where_condition]
    [GROUP BY {col_name|expr|position}]
    [HAVING where_condition]
    [ORDER BY {col_name|expr|position}]
```

```mariadb
SELECT 열이름
FROM 테이블이름
WHERE 조건
```

---

### `use`구문

```mariadb
USE 데이터베이스_이름;
```

* 사용할 DB를 설정하는 구문
* 다른 DB를 사용하겠다 명시하지 않으면 같은 DB사용
* HeidiSQL 에서는 클릭으로 해결

---

```mariadb
SHOW DATABASES ;-- 현재서버에 어떤 데이터베이스가 있는지 조사

USE 데이터베이스이름 ; -- 데이터베이스 지정

SHOW TABLE STATUS; -- 현재의 데이터베이스에 있는 테이블의 정보를 조회
/*SHOW TABLES; 테이블이름만 간단히 볼때 사용*/ 

DESCRIBE 테이블이름 ; -- 테이블의 열이 무엇이 있는지 확인(==DESC 테이블이름;)

SELECT 원하는 데이터 FROM 테이블이름; -- 원하는 데이터만 조회

SELECT COUNT(*) FROM 테이블이름; -- 테이블에 몇개의 데이터가 있는지 조회

SELECT * FROM 테이블이름 LIMIT 20; -- 테이블에서 20줄의 데이터만 조회(원하는 숫자 변경)
```

---

> 실습

```mariadb
DROP DATABASE if EXISTS sqlDB; -- 만약 sqlDB가 있으면 우선 삭제(경고창무시)
CREATE DATABASE sqlDB; -- 데이터베이스 생성

USE sqlDB;
CREATE TABLE userTbl -- 회원 테이블 
( userID  	CHAR(8) NOT NULL PRIMARY KEY, -- 사용자 아이디(PK)
  name    	VARCHAR(10) NOT NULL, -- 이름 
  birthYear   INT NOT NULL,  -- 출생년도 
  addr	  	CHAR(2) NOT NULL, -- 지역(경기,서울,경남 식으로 2글자만입력) 
  mobile1	CHAR(3), -- 휴대폰의 국번(011, 016, 017, 018, 019, 010 등) 
  mobile2	CHAR(8), -- 휴대폰의 나머지 전화번호(하이픈제외)
  height    	SMALLINT,  -- 키 
  mDate    	DATE  -- 회원 가입일 
);
CREATE TABLE buyTbl -- 회원 구매 테이블 
(  num 		INT AUTO_INCREMENT NOT NULL PRIMARY KEY, -- 순번(PK)
   userID  	CHAR(8) NOT NULL, -- 아이디(FK)
   prodName 	CHAR(6) NOT NULL, --  물품명 
   groupName 	CHAR(4)  , -- 분류 
   price     	INT  NOT NULL, -- 단가 
   amount    	SMALLINT  NOT NULL, -- 수량 
   FOREIGN KEY (userID) REFERENCES userTbl(userID)
);


INSERT INTO userTbl VALUES('LSG', N'이승기', 1987, N'서울', '011', '11111111', 182, '2008-8-8'); -- insert문을 이용하여 직접 데이터를 입력
INSERT INTO userTbl VALUES('KBS', N'김범수', 1979, N'경남', '011', '22222222', 173, '2012-4-4');
INSERT INTO userTbl VALUES('KKH', N'김경호', 1971, N'전남', '019', '33333333', 177, '2007-7-7');
INSERT INTO userTbl VALUES('JYP', N'조용필', 1950, N'경기', '011', '44444444', 166, '2009-4-4');
INSERT INTO userTbl VALUES('SSK', N'성시경', 1979, N'서울', NULL  , NULL      , 186, '2013-12-12');
INSERT INTO userTbl VALUES('LJB', N'임재범', 1963, N'서울', '016', '66666666', 182, '2009-9-9');
INSERT INTO userTbl VALUES('YJS', N'윤종신', 1969, N'경남', NULL  , NULL      , 170, '2005-5-5');
INSERT INTO userTbl VALUES('EJW', N'은지원', 1972, N'경북', '011', '88888888', 174, '2014-3-3');
INSERT INTO userTbl VALUES('JKW', N'조관우', 1965, N'경기', '018', '99999999', 172, '2010-10-10');
INSERT INTO userTbl VALUES('BBK', N'바비킴', 1973, N'서울', '010', '00000000', 176, '2013-5-5');
INSERT INTO buyTbl VALUES(NULL, 'KBS', N'운동화', NULL   , 30,   2);
INSERT INTO buyTbl VALUES(NULL, 'KBS', N'노트북', N'전자', 1000, 1);
INSERT INTO buyTbl VALUES(NULL, 'JYP', N'모니터', N'전자', 200,  1);
INSERT INTO buyTbl VALUES(NULL, 'BBK', N'모니터', N'전자', 200,  5);
INSERT INTO buyTbl VALUES(NULL, 'KBS', N'청바지', N'의류', 50,   3);
INSERT INTO buyTbl VALUES(NULL, 'BBK', N'메모리', N'전자', 80,  10);
INSERT INTO buyTbl VALUES(NULL, 'SSK', N'책'    , N'서적', 15,   5);
INSERT INTO buyTbl VALUES(NULL, 'EJW', N'책'    , N'서적', 15,   2);
INSERT INTO buyTbl VALUES(NULL, 'EJW', N'청바지', N'의류', 50,   1);
INSERT INTO buyTbl VALUES(NULL, 'BBK', N'운동화', NULL   , 30,   2);
INSERT INTO buyTbl VALUES(NULL, 'EJW', N'책'    , N'서적', 15,   1);
INSERT INTO buyTbl VALUES(NULL, 'BBK', N'운동화', NULL   , 30,   2);


SELECT * FROM userTbl;
SELECT * FROM buyTbl;
```



### 특정한 조건의 데이터만 조회하는 `SELECT ~ FROM ~ WHERE`

```mariadb
SELECT 필드이름 FROM 테이블이름 WHERE 조건식;
```

> 실습

```mariadb
USE sqlDB;
SELECT * FROM userTbl;

SELECT * FROM userTbl WHERE NAME = '김경호'; -- user테이블에서 김경호란 이름 조회
```

* 관계 연산자이용

> 실습

```mariadb
SELECT userID , NAME FROM userTbl WHERE birthYear >= 1970 AND height >= 182;
-- 1970년 이후 출생이고 신장이 182 이상인 사람의 아이디와 이름 조회
SELECT userID , NAME FROM userTbl WHERE birthYear >= 1970 OR height >= 182;
-- 1970년 이후 출생이거나 신장이 182 이상인 사람의 아이디와 이름 조회
```

```mariadb
-- 키가 180 ~ 183인 사람 조회

SELECT NAME, height FROM userTbl WHERE height >- 180 AND height <= 183; 

SELECT NAME, height FROM userTbl WHERE height BETWEEN 180 AND 183;-- BETWEEN ~ AND 사용
```

```mariadb
-- 지역이 경남,전남,경북 인 사람의 정보 조회
SELECT NAME, addr FROM userTbl WHERE addr = '경남' OR addr='전남' OR addr='경북';

-- IN을 사용하면 한꺼번에 작성가능
SELECT NAME, addr FROM userTbl WHERE addr IN ('경남','전남','경북');
```

```mariadb
-- 성이 김씨이고 , 그 뒤는 무엇이든(%) 허용한다는 의미
SELECT NAME, height FROM userTbl WHERE NAME LIKE '김%'
-- 맨 앞글자가 한글자이고, 뒤가 종신인 것 조회
SELECT NAME, height FROM userTbl WHERE NAME LIKE '_종신';

-- '_용%' 처럼 두가지 조합해서 사용가능
```

---

### 서브쿼리

* 쿼리문 안에 또 쿼리문이 들어있는것
* 조건식의 필드가 같아야 한다 !(WHERE height == SELECT height)

```mariadb
SELECT Name, height FROM userTbl 
   WHERE height > (SELECT height FROM userTbl WHERE Name = '김경호');
```

#### ANY

* 서브쿼리의 여러 개의 결과중 한가지만 만족해도 OK
* SOME은 ANY와 동일한 의미

```mariadb
SELECT NAME, height FROM userTbl
	WHERE height >= ANY (SELECT height FROM userTbl WHERE addr = '경남');
```

#### ALL

* 서브쿼리의 여러개의 결과를 모두 만족시켜야함

```mariadb
SELECT NAME, height FROM userTbl
	WHERE height >= ALL (SELECT height FROM userTbl WHERE addr = '경남');
```

---

### 원하는 순서대로 정렬하여 출력 : `ORDER BY`

* 기본적으로 오름차순 정렬

```mariadb
SELECT NAME, mDate FROM userTbl ORDER BY mDate;
```

* 내림차순은 `DESC`

```mariadb
SELECT NAME, mDate FROM userTbl ORDER BY mDate DESC;
```

* 키가 큰 순으로 정렬하되, 키가 같을 경우 이름 순으로 정렬 

```mariadb
SELECT NAME, height FROM userTbl ORDER BY height DESC , NAME ASC;
```

---

### 중복된 것 하나만 남기는 `DISTINCT`

```mariadb
SELECT addr FROM userTbl; -- 주소 조회

SELECT addr FROM userTbl ORDER BY addr; -- 정렬

SELECT DISTINCT addr FROM userTbl; -- 중복제거하고 출력
```

---

### 출력하는 개수 제한하는 `LIMIT`

```mariadb
USE employees;
SELECT emp_no, hire_date FROM employees
	ORDER BY hire_date ASC
	LIMIT 5; -- 5개만 조회
```

---

### 테이블을 복사하는 `CREATE TABLE ~ SELECT`

```mariadb
CREATE TABLE 새로운 테이블 (SELECT 복사할 열 FROM 기존테이블)
```

```mariadb
USE sqlDB;
CREATE TABLE buyTbl2 (SELECT * FROM buyTbl);
SELECT * FROM buyTbl2;
```

---

### `GROUP BY` 및 `HAVING` , 집계함수

* 그룹으로 묶어주는 절

```mariadb
SELECT userID, amount FROM buyTbl ORDER BY userID; 

SELECT userID, SUM(amount) FROM buyTbl GROUP BY userID; -- 사용자 아이디별로 묶어준 뒤, sum()사용

SELECT userID AS '사용자아이디', SUM(amount) AS '총구매개수'
	FROM buyTbl GROUP BY userID; -- AS를 사용하여 이름변경
	
SELECT userID AS '사용자아이디',SUM(price*amount) AS '총 구매액'
	FROM buyTbl GROUP BY userID;
```

#### 집계함수

| 함수명          | 설명                                   |
| --------------- | -------------------------------------- |
| AVG()           | 평균을 구한다.                         |
| MIN()           | 최소값을 구한다.                       |
| MAX()           | 최대값을 구한다.                       |
| COUNT()         | 행의 개수를 센다.(NULL값은 빼고 센다.) |
| COUNT(DISTINCT) | 행의 개수를 센다.(중복 1개만 인정)     |
| STDEV()         | 표준편차를 구한다.                     |
| VAR_SAMP()      | 분산을 구한다.                         |

> 실습

```mariadb
USE sqlDB;
SELECT AVG(amount) AS '평균 구매 개수' FROM buyTbl;
SELECT NAME, MAX(height), MIN(height) FROM userTbl GROUP BY NAME;
SELECT COUNT(mobile) AS '휴대폰이 있는 사용자' FROM userTbl;
```

---

### `HAVING`절 

* 집계함수는 `WHERE`절에 나타낼 수 없음
* **HAVING**은 WHERE 과 비슷한 개념
* 반드시 **`GROUP BY`** 다음에 와야한다.

```mariadb
SELECT userID AS '사용자',SUM(price*amount) AS '총 구매액'
	FROM buyTbl
	GROUP BY userID
	HAVING SUM(price*amount) > 1000
	ORDER BY SUM(price*amount);
```

---

### `ROLLUP`

* 총합 또는 중간합계가 필요할 떄 **GROUP BY** 절과 함께 **WITH ROLLUP** 사용

```mariadb
SELECT num, groupName, SUM(price*amount) AS '비용'
	FROM buyTbl
	GROUP BY groupName, num
	WITH ROLLUP;
```

* num(PK) 으로 그룹화 하여 중간중간에 소합계가 출력

  * 소합계 및 총합계만 필요하면 num 빼면됨

  ```mariadb
  SELECT num, groupName, SUM(price*amount) AS '비용'
  	FROM buyTbl
  	GROUP BY groupName
  	WITH ROLLUP;
  ```

  >실행하여 확인

---

### 데이터 삽입 : `INSERT`

```mariadb
INSERT [INTO] 테이블[(열1,열2,...)] VALUES(값1,값2,...)
```

### 자동으로 증가하는 `AUTO_INCREMENT`

* **AUTO_INCREMENT** 로 지정할 때는 꼭 **PRIMARY KEY** 또는 **UNIQUE**로 지정해 줘야한다.
* 데이터 형식은 숫자형식만 가능

```mariadb
USE sqlDB;
CREATE TABLE testTBL2
	(id INT AUTO_INCREMENT PRIMARY KEY,
	 userName CHAR(3),
	 age INT);
INSERT INTO testTBL2 VALUES (NULL,'지민',25);
INSERT INTO testTBL2 VALUES (NULL,'유나',22);
INSERT INTO testTBL2 VALUES (NULL,'유경',21);
SELECT * FROM testTBL2;
```

* **AUTO_INCREMENT** 의 입력값 지정할 때

```mariadb
ALTER TABLE testTBL2 AUTO_INCREMENT = 100; -- 시작값을 100으로 지정
INSERT INTO testTBL2 VALUES (NULL,'찬미',23);
SELECT * FROM testTBL2;
```

* 초기값 ,증가값 지정

```mariadb
USE sqlDB;
CREATE TABLE testTBL3
	(id INT AUTO_INCREMENT PRIMARY KEY,
	 userName CHAR(3),
	 age INT );
ALTER TABLE testTBL3 AUTO_INCREMENT = 1000; -- 시작값을 1000으로 지정
SET @@AUTO_INCREMENT_increment = 3; -- 증가값을 3으로 지정
INSERT INTO testTBL3 VALUES(NULL,'나연',20);
INSERT INTO testTBL3 VALUES(NULL,'정연',18);
INSERT INTO testTBL3 VALUES(NULL,'모모',19);
SELECT * FROM testTBL3;
```

* 대량의 샘플 데이터 생성
  * 다른 테이블의 데이터를 가져와서 대량으로 입력하는 효과

```mariadb
INSERT INTO 테이블이름 (열이름1,열이름2,...)
	SELECT문;
```

---

### 데이터 수정 :`UPDATE`

```mariadb
UPDATE 테이블이름
	SET 열1=값1,열2=값2 ...
	WHERE 조건
```

```mariadb
UPDATE testTBL4
	SET Lname = '없음'
	WHERE Fname = 'Kyoichi'
```

---

### 데이터 삭제  : `DELETE`

* 트랜잭션 로그에 기록되어 성능은 좋지 않다.

```mariadb
DELETE FROM 테이블이름 WHERE 조건;
```

```mariadb
USE sqlDB;
DELETE FROM testTBL4 WHERE Fname = 'Aamer';
```

#### 대용량의 테이블 전체 내용을 삭제할 때 , 테이블 자체가 필요없을 때는 `DROP`

#### 테이블의 구조는 남기고 싶으면 `TRUNCATE`

* 트랜잭션 로그 기록이 남지 않음

---





