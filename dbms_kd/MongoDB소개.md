# MongoDB

### NoSQL

* 분산 System, 병렬 System 지원
  * RDBMS가 하나의 server를 이용해 관리한다면, NoSQL은 server가 여러개 있다고 생각

* SQL(**CRUD** : Create,Read,Update,Delete 같은) 언어사용 X
  * 언어가 다름

#### 장점

* 클라우드 컴퓨팅 환경에 적합하다.
  * Open Source 이다
  * 하드웨어 확장에 유연하다
  * RDBMS에 비해 저렴한 비용으로 분산,병렬 처리가 가능
* 유연한 데이터 모델이다.
  * 비정형 데이터 구조 설계로 설계 비용감소
  * RDBMS보다 속도가 빠르다
* Big data 처리에 효과적
  * Memory Mapping 기능을 통해 Read/Write 가능
  * 전형적인 OS 와 Hardware에 구축가능
  * 기존 RDBMS와 동일하게 데이터처리가 가능

---

#### CAP 이론

* 어떠한 분산 시스템도 **일관성(Consistency) , 가용성(Availabilty) , 지속성(Partition tolerance)** 중 3가지를 만족시킬 수 없다는 이론
* **일관성(Consistency)**
  * 모든 노드들은 같은 시간에 동일한 항목에 대해 같은 내용의 데이터를 보여준다.
* **가용성(Availability)**
  * 모든 사용들이 읽기 및 쓰기가 가능해햐 하고, 몇몇 노드가 장애가 생겨도 다른 노드에 영향을 미치면 안됨
* **지속성(Partition tolerence)** 
  * 메세지 전달이 실패하거나 시스템 일부가 망가져도 시스템이 계속 동작할 수 있어야 한다.
* CA
  * Oracle, MySQL, SQL Server, Sybase
* AP
  * Dynamo, Casandra, CouchDB, SimpleDB
* CP
  * MongoDB, HBase , BerkeryDB

---

#### HDFS(Hadoop Distributed File System)

* **저 비용 하드웨어를 이용**하여 빅데이터를 효율적으로 처리하기 위한 **분산 파일 시스템**을 의미
* **수평적 확장**을 통한 시스템의 가용성을 극대화 시킬 수 있으며, 기종 간의 하드웨어와 소프트웨어 플랫폼의 **이식성**이 뛰어나다.



#### MapReduce

* 구글에서 분산 컴퓨팅을 지원하기 위한 목적으로 제작
* 클러스터 환경에서 병렬처리하기위해 개발
  * MAP과 REDUCE 함수로 구성
* **MAP 함수** 를 통해 Input 데이터(key:value)를 여러개 작은 split-peace로 분산입력하고 , **REDUCE 함수**를 통해 중복 데이터를 제거한 후 사용자가 원하는 형태로 데이터를 집게
* 구글 MapReduce를 기반으로 Hadoop MapReduce가 설계되고, Hadoop HDFS를 통해 수집 저장된 빅데이터의 효과적인 분석처리를 위한 프로그램 모델들이다.

---

### MongoDB

* JSON type의 형태로 데이터 저장구조제공
* Sharding(분산) , Replica(복제) 기능 제공
* MapReduce(분산/병렬처리) 기능 제공
* CRUD 위조의 다중 트랜잭션 처리도 가능
* Memory Mapping 기술 기반으로 빅데이터 처리에 탁월한 성능 제공
* 대소문자 구분 해야함



* C:\> mkdir c:\mongodb\test
* C:\MONGODB> mongod --dbpath c:\mongodb\test -> MongoDB 인스턴스 활성화(서버활성화)
* C:\MONGODB> mongo localhost : 27017 (다른 명령 프롬프르에서) : 서버 접속
* `show dbs` : show databases
* `use test` : test 란 db를 사용한다.

* `db.stats()` : db에 관련된 전반적인 정보 출력

```shell
>db.stats()
 {
        "db" : "show",          <-DB명
        "collections" : 0,      <-컬렉션 수
        "views" : 0,            <-뷰어의 수
        "objects" : 0,          <-오브젝트 수
        "avgObjSize" : 0,       <-오브젝트의 평균 크기
        "dataSize" : 0,         <-데이터 크기
        "storageSize" : 0,      <-저장공간의 크기
        "numExtents" : 0,       <- 총 익스턴트 수
        "indexes" : 0,          <- 인덱스 수
        "indexSize" : 0,        <- 인덱스 크기
        "fsUsedSize" : 0,       <- 사용된 파일 크기
        "fsTotalSize" : 0,      <- 총 파일 크기
        "ok" : 1                <- 문장의 실행 상태(정상:1,  실패:0) 
}
```

* `db.shutdownServer()` : 인스턴스까지 종료
* `db.logout()` : 인스턴스를 살아있고 , 클라이언트의 접속만 해제
* `exit`
* `db.hostInfo()` : 호스트 정보 출력

```shell
{
        "system" : {
                "currentTime" : ISODate("2021-01-22T04:22:03.724Z"), <- 표준시간
                "hostname" : "sw0329", 
                "cpuAddrSize" : 64,
                "memSizeMB" : NumberLong(7865),
                "memLimitMB" : NumberLong(7865),
                "numCores" : 8,
                "cpuArch" : "x86_64",
                "numaEnabled" : false
        },
        "os" : {
                "type" : "Windows",
                "name" : "Microsoft Windows 10",
                "version" : "10.0 (build 19042)"
        },
        "extra" : {
                "pageSize" : NumberLong(4096),
                "physicalCores" : 4
        },
        "ok" : 1
}
```

---

| RDBMS           | NoSQL                                |
| --------------- | ------------------------------------ |
| Primary Key     | _ID Field                            |
| Column          | BSON Field                           |
| Table           | Collection                           |
| Row             | Bson Document                        |
| RelationShip    | Embedded & Linking                   |
| create 테이블명 | db.createCollection(컬렉션명,설정값) |

#### Collection 생성

* RDBMS에서 테이블에 해당되는 역할을 MongoDB에서는 **컬렉션(Collection)**으로 표현
* Collection을 생성할 때 필드명, 데이터 타입 등 구성요소가 설정되지 않아도 데이터 저장구소 생성

##### Non Capped Collection

* 관계형 DB처럼 허용하는 범위 내에서 데이터를 계속적으로 저장할 수 있는 타입
* 범위가 다 차면 같은 크기의 Collection을 새롭게 계속 만듬
* `capped : false`

##### Capped Collection

* 최초 제한된 크기로 생성된 공간(익스텐트) 내에서만 데이터를 저장 가능
* 만약 최초공간이 모두 사용되면 다시 처음으로 돌아가서 기존 공간을 재사용
  * 로그 데이터처럼 일정기간내에서만 저장,관리가 필요한 데이터에 효과적
* 컬렉션이 꽉 차면 다시 처음으로 돌아가서 overwrite됨 
* `capped : true`

```shell
> use 테이블이름 --> 가능

> db.createCollection ("employees" , {capped: true, size: 100000 })
 --> employ라는 컬렉션 생성(size는 100000에 capped Collection생성)
 
> db.employees.renameCollection("emp") --> 컬렉션 이름 변경

> db.emp.drop() --> 컬렉션 삭제
```

---

### 데이터 Collection

#### 입력(save,insert)

```shell
> use DB이름
> m = {key : value} --> JSON 타입으로 입력
> db.컬렉션이름.save(m) --> 변수를 받아서 저장
> db.컬렉션이름.find() --> Collection에 저장된 데이터를 검색할 때 FIND 사용
> db.컬렉션이름.insert({key : value},{key : value}...) 
```

```shell
> use test
> m={ename : "smith"}    <- MongoDB에서는 JSON 타입으로 데이터를 표현
> n={ empno : 1101 }
> db.things.save(m)  <- 데이터를 저장할때 SAVE 함수를 사용
> db.things.save(n)
> db.things.find()   <- Collection에 저장된 데이터를 검색할 때 FIND 매쏘드 실행
> db.things.insert({ empno : 1102, ename : "king"})   <- 데이터를 입력할때 INSERT 함수를 사용
> db.things.find()
> show collections --> 컬렉션 만들지 않아도 자동으로 생성

===================================================================================

> for (var n = 1103; n <= 1120; n++) db.things.save({n : n , m : "test"})


> db.things.find()    <- FOR 반복문을 통해 증가된 값을 n 필드에 적용하여 데이터를 저장


> it      <- 출력된 결과가 20개를 초과하면 it 명령어로 다음 화면으로 이동
```

#### 수정(UPDATE)

```shell
=============================================================
============  데이터 수정하기 ===============================


> db.things.update({n:1103}, { $set: {ename : "standford", dept : "research"}})
> db.things.update({n:1104}, { $set: {ename : "John", dept : "inventory"}})
> db.things.update({n:1105}, { $set: {ename : "Jeo", dept : "accounting"}})
> db.things.update({n:1106}, { $set: {ename : "king", dept : "research"}})
> db.things.update({n:1107}, { $set: {ename : "adams", dept : "personel"}})
> db.things.update({n:1108}, { $set: {ename : "blake", dept : "inventory"}})
> db.things.update({n:1109}, { $set: {ename : "smith", dept : "accounting"}})
> db.things.update({n:1110}, { $set: {ename : "allen", dept : "research"}})
> db.things.update({n:1119}, { $set: {ename : "clief", dept : "human resource"}})
> db.things.update({n:1120}, { $set: {ename : "miller", dept : "personel"}})

>
> db.thing.save({empno : 1101, ename : "Blake", dept : "account"})
                                    
                             <- 이미 입력된 데이터를 변경할 때는 SAVE 함수보다는 UPDATE 함수를 사용하는 것이 유리
```

#### 삭제(remove)

```shell
> db.things.remove({m : "test"})
> db.things.find()
> db.things.remove({})
> db.things.find()
> db.things.drop()
```

#### SQL 과 Mongo

> ppt 참고(p66)



#### SAVE,INSERT,UPDATE

* INSERT
  * Collection에 하나의 Document를 최초 저장할 때 일반적으로 사용되는 메서드
* UPDATE
  * 하나의 Dcoument에서 특정 필드 만을 수정하는 경우 사용
  * 빠른 수정이 요구되는 경우 가장 적합한 방법
* SAVE
  * 하나의 Document에서 특정 필드만 변경해도 Document단위로 데이터를 변경
  * Document단위는 효율적, 필드 단위는 UPDATE가 효율적

---

### 인덱스

* db문자열에 컬렉션명 ,`createindex`메서드로 생성
* 현재 컬렉션에 생성되어 있는 인덱스 종류와 개수를 확인할 때는 `getindexes`메서드 사용
* MongoDB에서 Index의 대소문자 엄격히 구분

> 보충설명 p90~

---

### Sharding(Partition)

* 가장 큰 목적은 파티셔닝을 통한 데이터 분산 처리와 성능 향상을 위한 Balancing
* 빅데이터의 효율적 관리와 백업 및 복구 전력 수립을 위한 솔루션
* Sharding System은 데이터의 적절한 분산처리를 통한 효율성 향상이 가장 큰 목적

---

