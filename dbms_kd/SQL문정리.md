# SQL문

> 기본적으로 대소문자 구문 X

### SELECT문

* 원하는 데이터를 가져와 주는 기본적인 `SELECT ... FROM`

```mariadb
SELECT 열이름
FROM 테이블이름
WHERE 조건
```



#### USE구문

* 사용할 데이터베이스 지정

```mariadb
USE 테이블이름;
```



#### SELECT와 FROM

```mariadb
SELECT * FROM TITLES; -- titles란 테이블에서 모든것을 조회하라
```

* 원하는 열만 조회가능

```mariadb
SELECT first_name FROM employees; -- employees테이블에서 사원의 이름만 조회

SELECT first_name,last_name gender FROM employees; -- 콤마(,)로 여러 열 한꺼번에 조회가능
```



#### 특정한 조건의 데이터만 조회하는 `SELECT ... FROM ... WHERE`

```mariadb
SELECT 필드이름 FROM 테이블이름 WHERE 조건식;
```

* EX

```mariadb
SELECT * FROM userTbl WHERE name = '김경호' -- user테이블에서 김경호만 전부 조회
```

* 관계 연산자도 사용가능

```mariadb
SELECT userID, Name FROM userTbl WHERE birthYear >= 1970 AND height >= 182;
-- 1970년 이후 출생, 신장 182 이상만 조회
```



#### `BETWEEN .. AND` 와 `IN()`, `LIKE`

* EX

```mariadb
SELECT Name, height FROM userTbl WHERE height BETWEEN 180 AND 183;

SELECT Name,height FROM userTbl WHERE name LIKE '김%'; -- 성이 김씨이고, 뒤에 무엇이든 허용(%)

SELECT Name, height FROM userTbl WHERE name LIKE '_종신';
-- 맨 앞에 한글자 이고, 뒤에가 종신인 것 조회
-- '_용%' 처럼 '_'와 '%' 혼용가능
```



#### `ANY/ALL/SOME` , 서브쿼리(하위쿼리)

* 서브쿼리란 쿼리문 안에 또 쿼리문이 들어있는 것이라고 생각
* ANY : 서브쿼리의 여러 개의 결과 중 한가지만 만족해도 됨
* ALL : 서브쿼리의 여러개의 결과를 모두 만족해야 한다

```mariadb
SELECT Name, height FROM userTbl
	WHERE height >= ANY (SELECT height FROM userTbl WHERE addr = '경남');
	
SELECT Name, height FROM userTbl
	WHERE height >= ALL (SELECT height FROM userTbl WHERE addr = '경남');	
```



#### 원하는 순서대로 정렬하여 출력하는 `ORDER BY`

* 결과에는 영향을 미치지 않지만 , 출력되는 순서를 조절하는 구문
* EX

```mariadb
SELECT * Name, mDate FROM userTbl ORDER BY mDate; -- mDate순서대로 출력

SELECT * Name, mDate FROM userTbl ORDER BY mDate DESC; -- 내림차순 정렬

SELECT * Name, mDate FROM userTbl ORDER BY mDate ASC; -- 오름차순 정렬
```



#### 중복되는 것 하나만 남기는 DISTINCT

* 중복을 모두 제거하고 하나씩만 출력
* EX

```mariadb
SELECT addr FROM userTbl ORDER BY addr;

SELECT DISTINCT addr FROM userTbl;
```



#### 출력개수 제한 : `LIMIT`

* EX

```mariadb
USE employees;
SELECT emp_no, hire_date FROM employees
	ORDER BY hire_date ASC -- 오름차순 정렬
	LIMIT 5; -- 상위 5명만 출력
```



#### 테이블 복사 : `CREATE TABLE ... SELECT`

* `SELECT *`을 사용하여 테이블 자체 복사 가능
* 원하면 필요한 일부 열을 지정해서 복사 가능

```mariadb
CREATE TABLE 새로운 테이블 (SELECT 복사할 열 FROM 기존 테이블)
```



#### `GROUP BY`, `HAVING` , 집계함수

#### 집계함수

| 함수명          | 설명                                 |
| --------------- | ------------------------------------ |
| AVG()           | 평균을 구한다.                       |
| MIN()           | 최소값을 구한다.                     |
| MAX()           | 최대값을 구한다.                     |
| COUNT()         | 행의 개수를 센다.                    |
| COUNT(DISTINCT) | 행의 개수를 센다(중복은 1개만 인정). |
| STDEV()         | 표준편차를 구한다.                   |
| VAR_SAMP()      | 분산을 구한다.                       |



#### GROUP BY

* 말 그대로 그룹으로 묶어주는 역할

* EX

```mariadb
SELECT userID, amount FROM buyTbl ORDER BY userID;
-- 사용자 별로 각각의 행이 별도로 출력됨

SELECT userID, SUM(amount) FROM buyTbl GROUP BY userID;
-- 집계함수와 GROUP BY절을 사용하여 SUM결과만 따로 출력됨

SELECT userID AS '사용자 아이디', SUM(price*amount) AS '총 구매액'
	FROM buyTbl GROUP BY userID;
-- AS를 이용해 이름을 바꿔주고, SUM함수안에서 곱하기`*` 사용가능
```



#### HAVING 절

* 집계함수를 사용하는 경우 `WHERE`사용 불가능
* 이와 비슷한 개념인 `HAVING`사용
* 반드시 **`GROUP BY`** 뒤에 와야한다.

```mariadb
SELECT userID AS '사용자', SUM(price*amount) AS '총 구매액'
	FROM buyTbl
	GROUP BY userID
	HAVING SUM(price*amount) > 1000; -- 총 구매액이 1000이상인 사람만 출력
```



#### `ROLL UP`

* 총합, 중간 합계 필요할 때 사용

```mariadb
SELECT num,groupName, SUM(price*amount) AS '비용'
	FROM buyTbl
	GROUP BY groupName
	WITH ROLLUP; -- 소합계,총합계 모두 출력(num제거하면 총합계만 출력)
```

---

### SQL 분류

#### DML(Data Manipulation Language,데이터 조작 언어)

* 데이터 조작하는데 사용하는 언어
* **SELECT,INSERT,UPDATE,DELETE**
* 트랜잭션을 발생시키는 언어
  * 테이블의 데이터를 변경할 때 실제 테이블에 적용하지 않고, 임시로 적용시키는 것이 트랜잭션
  * 실수가 발생할 때 수정가능

#### DDL(Data Definition Language,데이터 정의 언어)

* 데이터베이스,테이블,뷰,인덱스 드으이 데이터베이스 개체를 생성,삭제,변경하는 역할
* **CREATE,DROP,ALTER**
* 트랜잭션을 발생시키지 않는다

#### DCL(Data Control Language,데이터 제어 언어)

* 사용자에게 권한을 부여하거나 빼앗을 때 주로 사용하는 구문
* **GRANT,REVOKE,DENY**

---

### 데이터 삽입 : `INSERT`

```mariadb
INSERT [INTO] 테이블[(열1,열2,...)] VALUES (값1,값2,...)
```

* EX

```mariadb
USER sqlDB;
CREATE TABLE testTBL1 (id int, userName char(3),age int);
INSERT INTO testTBL1(userName,age,id) VALUES('초아',26,3);
```



#### 자동으로 증가하는 `AUTO_INCREMENT`

* 테이블 속성이 **AUTO_INCREMENT** 로 되어 있으면, INSERT에서는 해당 열이 없다고 생각하고 입력
* **AUTO_INCREMENT** 는 자동으로 1부터 증가하는 값을 입력
* **AUTO_INCREMENT** 로 입력할 때는 꼭 `PRIMARY KEY` OR `UNIQUE`로 지정해줘야 한다
* 데이터 형식은 숫자형만 가능
* INSERT할 때 NULL값으로 주면 자동으로 입력됨

```mariadb
USE sqlDB;
CREATE TABLE testTBL2
	(id int AUTO_INCREMENT PRIMARY KEY, userName char(3), age int);
INSERT INTO testTBL2 VALUES(NULL,'제니', 25);
INSERT INTO testTBL2 VALUES(NULL,'로제', 25);
INSERT INTO testTBL2 VALUES(NULL,'지수', 27);
SELECT * FROM testTBL2;
```

* 입력 시작값 변경 가능

```mariadb
ALTER TABLE testTBL2 AUTO_INCREMENT=100;
INSERT INTO testTBL2 VALUES(NULL,'리사',25);
SELECT * FROM testTBL2;
```

* 증가값 변경가능

```mariadb
USE sqlDB;
CREATE TABLE testTBL3
	(id int AUTO_INCREMENT PRIMARY KEY, userName char(3), age int);
ALTER TABLE testTBL3 AUTO_INCREMENT=1000;
SET @@auto_increment_increment=3' -- 3씩 증가로 증가값을 변경
INSERT INTO testTBL3 VALUES(NULL,'제니', 25);
INSERT INTO testTBL3 VALUES(NULL,'로제', 25);
INSERT INTO testTBL3 VALUES(NULL,'지수', 27);
SELECT * FROM testTBL3;
```



#### `INSERT IGNORE`

* PK가 중복되는 것처럼 오류가 생겨도 오류를 무시하고 데이터 입력

---

### 데이터 수정 : `UPDATE`

* 기존에 입력되어 있는 값을 변경하기 위해서는 **UPDATE문**
* WHERE절 생략가능 하지만 생락하면 테이블 전체의 행이 변경 됨

```mariadb
UPDATE 테이블이름
	SET 열1=값1,열2=값2;
	WHERE 조건;
```



#### `ON DUPLICATE UPDATE`

* PK가 중복되지 않으면 INSERT 수행
* PK가 중복되면 그 뒤의 UPDATE 문을 수행

---

### 데이터 삭제 : `DELETE FROM`

* DELETE는 행 단위로 삭제
* WHERE절이 생략되면 전체 데이터를 삭제

```mariadb
DELETE FROM 테이블이름 WHERE 조건;
```



#### DELETE, DROP , TRUNCATE

#### DELETE

* 트랜잭션을 로그에 기록하기 때문에 성능이 나쁨

#### DROP

* 대용량으로 테이블 전체 내용을 삭제할 때, 테이블 자체가 필요없을 경우 사용

#### TRUNCATE

* 테이블의 구조는 남겨 놓고 싶을 때 사용

---

### WITH 절

* 임시 테이블 생성하는 역할
* 동일한 SQL반복되어 사용될 때 사용

```mariadb
WITH CTE_테이블이름(열이름) AS (쿼리문)
SELECT 열이름 FROM CTE_테이블이름;
```

* EX

```mariadb
USE sqlDB;
SELECT userid AS '사용자', SUM(price*amount) AS '총 구매액'
	FROM buyTBL GROUP BY userid;
```

```mariadb
SELECT * FROM abc ORDER BY 총구매액 DESC
```

```mariadb
WITH abc(userid,total)
AS
(SELECT userid, SUM(price*amount))
	FROM buyTBL GROUP BY userid;
SELECT * FROM abc ORDER BY total DESC;
```



---

