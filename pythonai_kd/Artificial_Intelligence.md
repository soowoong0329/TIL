# Artificial Intelligence (인공 지능) :&#127760;

> 인공지능이란 인공장치(기계)들의 지능을 설계하는 것
>
> *MaCarthy , 1956*

#### 인공장치가 인간의 지능(행동)을 모방하는 것

#### 지능(Intelligence) : 인간이 행하는 지적 작업의 주체

* 생명체가 생존환경의 변화에 적응하기 위해 <span style="color:red">**인지적 기능**</span>을 변화시키는 능력

---

#### AI - Type

* **약한 인공지능**(A<span style="color:red">N</span>I : Artificial <span style="color:red">Narrow</span> Intelligence) == 특화지능
  * 많은 양의 데이터를 처리하여 <span style="color:red">**특정기능**</span>만 수행
  * 현재 약한 인공지능 시대에 살고 있다.
    * Weak의 뜻이 아닌, Narrow의 뜻
    * ex) 알파고가 바둑은 잘 두지만, 다른 일은 하지 못함



* **강한 인공지능**(A<span style="color:blue">G</span>I : Artificial <span style="color:blue">General</span> Intelligence)
  * 사람처럼 생각하고 판단하는 <span style="color:blue">범용</span> 인공지능



* **특이점**(Singularity)
  * 인간과 인공지능 사이의 임계점



* **슈퍼 인공지능**(ASI : Artificial Super Intelligence)
  * 특이점을 지나 인간의 지능을 넘어선 인공지능

#### Turing Test

* 튜링 테스트
  
* **컴퓨터가 지능을 가지고 있는지** 여부 조사
  
* 질문자가 인간과 컴퓨터에게 **같은 질문**을 하여 인간의 답과 컴퓨터의 **답을 구분할 수 없으면**

  컴퓨터가 **지능을 가진 것**으로 볼 수 있음

* CAPTCHA

---

#### AI :question:

* Intelligence
  * 사람의 지적작업
  * 예측(predict)
    * regression : 수치예측
    * classification : 분류

* **Machine Learning** : 데이터로부터 일관된 패턴 또는 새로운 지식을 찾아내는 방법
  
  * Machine : <span style="color:blue">**수학의 함수(Function)**</span> 
  
  * Learning : <span style="color:blue">**변화(Change)**</span>
  
  * Parameter를 주어진 데이터에 최적화(Optimization)시키는 것
  
  * <span style="color:darkgreen">Model : 학습이 된 함수(Function)</span>
  
  * 최적의 모델을 만들기 위해서 <span style="color:blue">**학습과 재학습**</span>을 반복하는 것
  
  * 기본적으로 학습(Learning)이라는 것은 행동의 <span style="color:blue">**Change(변화)**</span>
  
    * 학습 이후 <span style="color:red">**새로운데이터**</span>에 대하여 <span style="color:blue">**학습된 내용**</span>으로 처리하는 것
  
    $$
    y = ax + b
    $$
  
    * a,b를 변화시켜가면서(학습) 최적의 함수(Model,Algorithm)를 찾아가는 것
    * x,y 는 제공을 받는 것(Data)

---

* 측정
  * 정성적 : 크다,많다,좋다,빠르다
  * 정량적 : 2개틀림, 30보다 작음

#### 지도학습(Supervised Learning) 

* 데이터에 존재하는 특징을 바탕으로 처리(수치예측, 범주예측)
* Input(x)에 대한 Output(y)을 제공
* **Input(x) Data 와 Output(y) Data(Label)의 관계를 학습**

#### 비지도학습(Unsupervised Learning)

* 데이터에 존재하는 특징(feature)을 확인(군집,연관)
* Input(x) Data만 제공
* 일반적으로 지도학습을 위한 <span style="color:red">**전처리 작업**</span>으로 수행

| 지도학습 알고리즘                                      | 비지도학습 알고리즘             |
| ------------------------------------------------------ | ------------------------------- |
| 회귀분석(Regression Analysis)                          | 주성분 분석(PCA)                |
| 로지스틱회귀(Logistic Regression)                      | k-평균 군집(K-means-Clustering) |
| 의사결정 나무(Decision Tree)                           | 연관 규칙(Association Rule)     |
| 랜덤포레스트(Random Forest)                            |                                 |
| <span style="color:red">신경망</span>(Neural Networks) |                                 |

---

### Gradient(기울기) Descent(하강) :chart_with_downwards_trend:

$$
y = wx + b
$$

* w : 가중치 , b : 편향

#### Regression Analysis(수치 예측)

![](https://static.thenounproject.com/png/239043-200.png![image](https://user-images.githubusercontent.com/77090825/111031767-7cbbde80-844c-11eb-9933-83e9dfe3ea6e.png)
)

#### Loss Function()

* **실제 값과 예측값 차이**(오차)를 비교하는 지표

$$
y = wx + b (y :실제 값 , \hat y : 예측값 , L(y,\hat y) = (y - \hat y)^2
$$



* y는 지도학습의 Output(Label) , x는 Input Data

* MSE(Mean Squared Error)는 Loss 들의 평균
* **MSE**가 작아지는 쪽으로 학습(변경) 시키는 것이 좋다.



#### Cost Function() : MSE

* Cost(Mean Squared Error) 는 Loss 들의 평균

$$
Cost(y,\hat y) = mean(L(y,\hat y)) = mean((y - \hat y)^2) = mean((y -(wx+b))^2)
$$

* Cost Function() **값(MSE)을 최소**로 하는 **Parameter(w,b) 값을 찾는 것**이 목적 !

![](https://github.com/soowoong0329/TIL/blob/master/img/mse.PNG?raw=true)

* w : 실제로는 w도 바뀌기 때문에 공간 상에서 최소값을 찾아가는 느낌

* 미분 : 순간변화량 , 접선의 기울기

* 편미분 사용 !

  * **Parameter 값이 변경될 때 Cost Function() 값은 얼만큼 변화 되는가?**

* w = w - r * dw(경사값)

* b = b-r * db

  ### 경사하강법 : 어느 지점이라도 기울기를 빼주면 b 값이 경사(Gradient) 따라 하강(descent) 하며 작아져 error가 줄어들 것이다 !

* (b-기울기) 값을 b에 재할당 

* 기울기 값이 너무 크면 오차(error) 가 더 커질수도 있다.
* b - r(gamma) * 기울기(r(gamma) 값을 주어서 **조금씩 움직이면서 최소값**을 찾아감)
  * **Tunning(튜닝)** 이 필요하다 !
    * 0 ~ 1 사이의 값을 시도하면서 **가장 좋은 값을 찾아야 한다 **!
    * **Hyper prarameter**
      * Learning Rate(학습률)
      * Step size

---

