# Regression Analysis

![](https://www.tibco.com/sites/tibco/files/media_entity/2020-09/regression-analysis-diagram.svg)

> *source : https://www.tibco.com/reference-center/what-is-regression-analysis*

#### Supervised Learning - Regression Analysis

* 과거의 결과값을 기준으로 미래의 결과값(수치) 예측 하는 방법

* **y = wx + b**
  

* w 와 b 값을 추정한다.

* y : Output(**종속변수**, 반응변수) , x : Input(**독립변수** , 설명변수)



## Scaling

* 데이터 전처리 과정 중 하나이다.
* 범위(Scale)가 다른 변수들의 **범위를 비슷**하게 맞추기 위한 목적

* 연속형 변수가 다양한 범위로 존재할 때, 제곱 오차 계산 시 왜곡이 발생할 수 있다.
  * ex ) X1 = 1 ~ 10, X2 = 100 ~ 1000 같은 경우

```python
from sklearn.preprocessing import MinMaxScaler

from sklearn.preprocessing import StandardScaler
```



### Normalization(정규화)

* 변수의 스케일을 **0 ~ 1 사이의 범위**로 맞추는 것(min - max scaling)
* 정규화는 변수의 범위가 정해진 값이 필요할 때 유용

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT21_4ihj7YOjvgUXd792eDP7NYX0Uoux7ZAQ&usqp=CAU)



### Standardization(표준화)


* 데이터가 평균으로부터 얼마나 떨어져 있는지?

* 변수의 평균을 0 , 표준편차를 1로 만들어 **표준정규분포**의 특징을 갖게 함
* 표준화는 가중치 학습을 더 쉽게 할 수 있도록 함
* 특정 범위를 벗어난 데이터는 outlier로 간주하고 제거한다.

![](https://www.oreilly.com/library/view/hands-on-machine-learning/9781788393485/assets/7a9d8cb9-10f7-43b5-b52f-865fbbb0b69e.png)

---

### 단일 회귀 분석

* 독립변수가 1개
* y = wx + b



### 다중회귀분석 

* 독립 변수가 여러개

---

> 실습 : Regression_Analysis in drive

