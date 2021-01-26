# SQL문

> MariaDB데이터 형식
>
> 숫자데이터형식,문자데이터형식,날짜와 시간데이터형식, 기타데이터 형식
>
> 책 참고(p.223),(google)



#### LONGTEXT,LONGBLOB

* MariaDB에서는 LOB(Large Object,대량의데이터) 를 저장하기위해 데이터 형식을 지원



#### 변수의 사용

* SQL도 변수 선언하고 사용가능

```mariadb
SET @변수이름 = 변수 값; -- 변수의 선언 및 값 대입
SELECT @변수이름 ; -- 변수의 값 출력
```



#### 데이터 형식 변환(`CAST()`,`CONVERT()`)

```mariadb
CAST (expression AS 데이터형식 [(길이)])
CONVERT ( expression, 데이터형식 [(길이)])
```

* EX

```mariadb
USE sqlDB;
SELECT AVG(amount) AS '평균구매 개수' FROM buyTBL;
SELECT CAST(AVG(amount) AS SIGNED INTEGER) AS '평균 구매 개수' FROM buyTBL;
-- or
SELECT CONVERT(AVG(amount),SIGNED INTEGER) AS '평균 구매 개수' FROM buyTBL;
```

```mariadb
-- 4개 값 모두 동일
SELECT CAST('2022$12$12' AS DATE);
SELECT CAST('2022/12/12' AS DATE);
SELECT CAST('2022@12@12' AS DATE);
SELECT CAST('2022%12%12' AS DATE);
```



---

### MariaDB 내장함수

> 책 참고(p.234),google

---

### 피벗, JSON

> p.262

#### 피벗

* 한 열에 포함된 여러 값을 출력하고, 이를 여러 열로 변환하여 테이블 반환 필요하면 집계까지 수행



#### JSON

* JavaScript Object Notation
* **{속성(key) : 값(value)}** 로 구성

---

# 조인

* 두 개 이상의 테이블을 서로 묶어서 하나의 결과 집합으로 만들어 내는 것
* 분리된 테이블들은 관계를 가짐

## INNER JOIN(내부 조인)

* 조인 중에 가장많이 사용되는 조인
* 대개의 업무에서 조인은 **INNER JOIN**사용
* 예
  * 물건을 배송하기 위해서는 구매한 회원의 주소필요
  * 회원의 주소 정보를 알기 위해 주소 정보가 있는 회원 테이블과 결합하는 조인이 **INNER JOIN**

```mariadb
SELECT <열 목록>
FROM <첫 번째 테이블>
	INNER JOIN <두 번째 테이블>
	ON <조인될 조건>
WHERE 검색조건
```

```mariadb
-- 구매테이블 중에서 JYP라는 아이디를 가진 사람이 구매한 물건을 발송하기 위해 이름/주소/연락처 등을 조인
USE sqlDB;
SELECT *
	FROM buyTBL
		INNER JOIN userTBL
			ON buyTBL.userID = usertbl.userID
	WHERE buytbl.userID = 'JYP';
```



#### 세 개 테이블 조인

* 이론적으로 다대다 관계
* 두 테이블 사이에 연결 테이블을 두어 연결테이블과 데이터 테이블이 일대다 조인을 맺을 수 있도록 처리

> 실습
>
> * 학생 기준으로 학생 이름/지역/가입한 동아리/동아리방 출력(p271)

---

## OUTER JOIN (외부 조인)

* 조인의 조건에 만족되지 않는 행까지도 포함시키는 것
* 형식

```mariadb
SELECT <열 목록>
FROM <첫 번째 테이블(LEFT 테이블)>
<LEFT | RIGHT | FULL > OUTER JOIN <두 번째 테이블(RIGHT 테이블)>
	ON <조인될 조건>
[WHERE 검색조건];
```

* LEFT OUTER JOIN(== LEFT JOIN)
  * 왼쪽 테이블 데이터 모두 출력
* FULL OUTER  JOIN (==FULL JOIN)
  * 양쪽 모두에 조건이 일치하지 않는 것 모두 출력

> 실습

```mariadb
USE sqlDB;
SELECT U.userID, U.name, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2)  AS '연락처'
   FROM userTBL U
      LEFT OUTER JOIN buyTBL B
         ON U.userID = B.userID 
   ORDER BY U.userID;

SELECT U.userID, U.name, B.prodName, U.addr, CONCAT(U.mobile1, U.mobile2)  AS '연락처'
   FROM buyTBL B 
      RIGHT OUTER JOIN userTBL U
         ON U.userID = B.userID 
   ORDER BY U.userID;
```

---

## SELF JOIN(자체조인)

* 자기 자신과 자기 자신이 조인
* 조직도 관련 테이블같은 경우 사용

> 실습

* 데이터생성

```mariadb
USE sqlDB;
CREATE TABLE empTbl (emp CHAR(3), manager CHAR(3), empTel VARCHAR(8));

INSERT INTO empTbl VALUES(N'나사장',NULL,'0000');
INSERT INTO empTbl VALUES(N'김재무',N'나사장','2222');
INSERT INTO empTbl VALUES(N'김부장',N'김재무','2222-1');
INSERT INTO empTbl VALUES(N'이부장',N'김재무','2222-2');
INSERT INTO empTbl VALUES(N'우대리',N'이부장','2222-2-1');
INSERT INTO empTbl VALUES(N'지사원',N'이부장','2222-2-2');
INSERT INTO empTbl VALUES(N'이영업',N'나사장','1111');
INSERT INTO empTbl VALUES(N'한과장',N'이영업','1111-1');
INSERT INTO empTbl VALUES(N'최정보',N'나사장','3333');
INSERT INTO empTbl VALUES(N'윤차장',N'최정보','3333-1');
INSERT INTO empTbl VALUES(N'이주임',N'윤차장','3333-1-1');
```

* SELF JOIN

```mariadb
SELECT A.emp AS '부하직원' , B.emp AS '직속상관', B.empTel AS '직속상관연락처'
   FROM empTbl A
      INNER JOIN empTbl B
         ON A.manager = B.emp
/*WHERE A.emp = '우대리';*/
```

---

## UNION/ UNION ALL / NOT IN / IN

#### UNION/UNION ALL

* 두 쿼리의 결과를 행으로 합치는 것
* 두 테이브르이 열의 개수가 같아야 한다
* 열의 데이터 형식도 호환되거나 같아야한다.
* 중복된 열 제거되어 출력
  * UNION ALL 쓰면 중복된 열 까지 출력

#### NOT IN

* 첫번째 쿼리의 결과 중 두 번쨰 쿼리에 해당하는 것을 제외하기 위한 구문
  * EX)테이블 사용자 모두 조회하되, 전화 없는 이 제외

```mariadb
SELECT name, CONCAT(mobile1, mobile2) AS '전화번호' FROM userTBL
   WHERE name NOT IN ( SELECT name FROM userTBL WHERE mobile1 IS NULL) ;
```

#### IN

* 첫번째 쿼리의 결과 중 두 번쨰 쿼리에 해당하는 것만 출력
  * EX) 테이블 사용자를 모두 조회해 전화 없는 이만 출력

```mariadb
SELECT name, CONCAT(mobile1, mobile2) AS '전화번호' FROM userTBL
   WHERE name IN ( SELECT name FROM userTBL WHERE mobile1 IS NULL) ;
```



