# Statistics :bar_chart:

### Descriptive Statistics : 기술통계

* (Descriptive)기술 : 적는것

* 통계 : 데이터를 수집 및 정리하여 **특징을 확인**하는 것

* 통계학에서 최종적으로 알고 싶은 것 : **모집단의 특징**

* 특징 : **중심화 경향치** : 모여있는 특징

  ​         : **산포도** : 퍼져(떨어져) 있는 특징

* 모집단의 **특징**을 알기 위해 데이터를 수집, 분석, 시각화

| 통게변수            | 통계 척도(Scale)  | 연산         |
| ------------------- | ----------------- | ------------ |
| 범주형 변수(정성적) | 명목형(명명) 척도 | ==, !=       |
|                     | 순서형(서열) 척도 | >, <, >=, <= |
| 수치형 변수(정량적) | 이산형(등간) 척도 | +,-          |
|                     | 연속형(비율) 척도 | *,/          |

* 명명(Nominal) : 측정값이 같고 다름만 확인, 측정값 사이에 순서없음
* 서열(Ordinal) : 측정값 사이에 순서가 있지만, 간격이 동일하지 않음
* 등간(Interval) : 측정값 사이에 순서가 있고, 간격이 동일/영점(0)의 의미 임의적
* 비율(Ratio) : 절대영점(아무것도 존재하지 않는 상태) 존재, 사칙연산 모두 가능



#### 중심화 경향치 (Measure of Central Tendency)

* 집단을 **대표**하는 값 :question:
* **무엇을 중심으로 모여 있는가?** :star:
*  평균
  * 전체 데이터를 더한 다음 전체 데이터 개수로 나눈 값
  * 이상치(Outlier) : 평균에 급격하게 영향을 주는 것
* 중앙값 : 전체 데이터를 크기 순으로 정렬하여 순서상 중앙에 위치한 값
* 최빈값 :  전체 데이터에서 가장 빈번하게 나타나는 값



#### 산포도(Degree of Dispersion)

* 집단 내 데이터가 흩어져 있는 정도
* 범위 : 수치형 연속변수 값의 최솟값과 최댓값 사이의 거리
  * 범위 = 최댓값 - 최솟값
  * 이상치를 포함
* 사분위범위 : 0%(최소값), 25%, 50%(중앙값), 75%, 100%(최대값) 구간으로 나눈 사분위수 25% ~ 75% 사이의 값들(boxplot으로 표현)

![](https://naysan.ca/wp-content/uploads/2020/06/box_plot_ref_needed.png)

> *source : https://naysan.ca/wp-content/uploads/2020/06/box_plot_ref_needed.png*

* 분산(Variance)

  * 관측치들이 **평균에서 평균적으로 얼마나 떨어져 있는지** 확인
    $$
    Variance = \sum(x_i - m)^2 \div n(모집단)
    $$

  * 표본집단 : n-1 로 나눠줌(자유도확인)

  * 일반적으로 모집단 모든 데이터를 가지고 있지 않고, 표본집단 데이터를 가지고 있기 때문에 n-1로 나눠줌

* 표준편차(Standard Deviation)
  * 분산의 양의 제곱근
  * 분산에 루트적용

---

### 확률 : Probability

|                      집합                       |                             확률                             |                             통계                             |
| :---------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|    <br>원소<br> 전체집합<br/> 부분집합<br/>     | 원소<br/> <span style = 'color:red'>표본공간</span><br/> <span style = 'color:blue'>사건</span><br/> | 데이터<br/> <span style = 'color:red'>모집단</span><br/> <span style = 'color:blue'>표본집단</span><br/> |
| 합집합<br/> 교집합<br/> 차집합<br/> 여집합<br/> |    덧셈정리<br/> 곱셈정리<br/> 독립<br/> 조건부확률<br/>     | <span style = 'color:red'>모집단분포</span><br/> <span style = 'color:blue'>확률변수</span><br/> 확률분포<br/>누적분포함수<br/> |



* 일정한 조건하에 어떤 사건(Event) 이 발생할 **가능성의 정도**
  * 수학적 확률 : 어떤 사람이 계산하여도 동일한 값으로 계산되는 확률
  * 통계적 확률 : 어떤 사건을 **독립시행으로 반복**했을 때 발생하는 확률
  * 주관적 확률 : 관찰자의 주관에 따라 다르게 표현되는 확률

* **확률은 비율(ratio)**
* 사건 A의 확률은 **0 <= P(A) <= 1**범위를 가짐
* 확률 = 특정 사건의 원소 개수 / 모든 사건의 원소 개수
  * 일반적으로 각각의 원소에 모두 같은 가중치를 부여한다고 생각
  * 서로 다른 가중치?
    * 홀수보다 짝수가 3배 더 발생하는 주사위
    * 홀수가 나올 확률 : s
    * 짝수가 나올 확률 : 3s
      * s * 3 + 3s * 3 = 1 --> 12s = 1 --> s = 1/12

#### 표본공간

* 통계에서 모집단과 같은 개념
* 통계적 실험에서 **발생 가능한 모든결과(원소)**들의 집합



#### 사건

* 표본공간의 **부분집합**
* **표본집단**과 같은 개념
* 사건은 표본공간(모집단)의 부분집합(표본집단)
* 사건은 표본공간 밖에서 만들어 질수 없다.



* 확률적 사건 : 표본공간에서 특정한 조건을 만족하는 결과들의 집합

| 사건                               | 설명                                         |
| ---------------------------------- | -------------------------------------------- |
| 전사건(Total Event)                | S의 모든 원소를 포함하는 사건(==전수조사)    |
| 공사건(Null Event)                 | S의 어떤 원소도 포함하지 않는 사건           |
| 여사건(Complementary Event)        | 사건 A에 포함되지 않는 S의 모든 원소         |
| 합사건(Union Event)                | 두 사건 A,B 중 적어도 한쪽에서 발생하는 사건 |
| 곱사건(Intersection Event)         | 두 사건 A,B에 동시에 발생하는 사건           |
| 배반사건(Mutually Exclusive Event) | 한 쪽에서만 발생하는 사건                    |



#### 확률변수(Random Variable)

* 확률변수
  * 확률적 법칙(사건) 에 따라 변화하는 값
  * 확률변수를 표본집단으로 간주
    * 이산적 확률변수 : 확률변수가 유한하게 존재(이산형)
    * 연속확률변수 : 확률변수가 연속적인 구간 내의 값을 취함(연속형)
  * 상태공간 : 확률변수가 취하는 모든 값의 집합 (표본집단이라고 생각)
    * 상태공간(확률변수 전체)을 구성하는 **각 값이 발생할 수 있는 확률**이 존재

#### 확률분포 (Probability Distribution)

* 확률분포
  * 확률변수 값과 각 값이 발생할 수 있는 확률을 대응 시킨 것
* 확률분포표
  * 확률분포를 표로 나타낸 것
* 확률 분포 함수 : 확률 변수 값이 발생 할 확률을 나타내는 함수
  * 확률분포 함수를 알고 있다면?
  * 어떤 **사건이 발생할 확률을 계산(예측) 가능**

#### 확률분포함수(Distribution Function)

* 이산형 : 확률**질량**함수 
* 연속형 : 확률**밀도함수**

![](data:image/png;base64,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)

* 누적분포함수
  * 확률변수 X의 누적분포함수
  * 확률변수 X에 대해서 확률변수 X가 특정값보다 작거나 같은 확률
  * F(x) = P(X<=x)

![](https://github.com/soowoong0329/TIL/blob/master/img/dist_func.PNG?raw=true)

* 누적분포 함수 종류
  * 이산형 : 확률질량함수
  * 연속형 : 확률밀도함수
  * 이항분포
  * 정규분포
  * 표준정규분포
* **모수(Parameter)** : 분포함수의 **모양**을 결정(평균,분산)

---

### 이항분포

#### 베르누이 시행

* 두 가지 결과가 나타나는 확률실험을 베르누이 시행이라고 한다.

  * p의 확률로 원하는 결과가 나오면 **성공**
  * (1-p)의 확률로 반대의 결과가 나타나면 **실패**

* 성공확률 p가 베르누이 시행의 **모수** : Bernoulli(p)

* 확률질량함수(이산형)

  P(X = x) = F(x) = p<sup>x</sup>(1-p)<sup>1-x</sup>



#### 이항분포

* 성공확률이 p로 동일한 베르누이 시행을 **n번 반복**
* 앞의 시행이 뒤에 할 시행에 영향을 주지 않는 독립 시행

* 이항분포

  B(n,p) = <sub>n</sub>C<sub>x</sub>p<sup>x</sup>(1-p)<sup>n-x</sup>

---

### 정규 분포

* 성공확률 0.5 , 시행횟수 n이 매우 큰 이항분포가 어떤 함수와 비슷해짐
* n이 매우 커지면 x가 이산형이 아닌 연속형처럼 다룰 수 있음

![](data:image/png;base64,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)

* 평균과 분산에 따라 모양이 달라진다.

![](https://upload.wikimedia.org/wikipedia/commons/1/1b/Normal_distribution_pdf.png)

* **표준변환(Z-transform)**에 의해 표준 정규분포로 변환가능

### 표준 정규 분포

* 평균 0 , 분산 1인 정규분포
* **Z = N(0,1)**

![](https://snappygoat.com/b/c85622872c1a807d09bbb4b233c03a50c2722928)

---

> t ,f , chi  distribution 참고

