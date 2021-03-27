# Regression Analysis

![](data:image/png;base64,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)

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

