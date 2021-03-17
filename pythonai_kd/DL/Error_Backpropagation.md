# Neural Network(2)

* Output Layer의 개수는 정해져 있다.

  * 회귀문제?
    * Output Layer : 1개
  * 분류문제?
    * Binary : 1개
    * Categorical(3개 이상) : 1000개면 1000개 , 100개면 100개 

* Binary Classification

  * w값들이 들어오게 되면 Sigmoid Activation을 통해 Output이 0과 1로 분류됨

* Categorical Classification

  * Output값이 1개가 아니라 여러개 이기 때문에 sigmoid activation을 사용하면,

    0 과 1로 표현 불가능

  * 0과 1로 표현이 가능한 **행렬**형태로 나타나게 함

    * 각각 output마다 sigmoid activation을 적용하여 0과 1로 나타내고, 이를 행렬로 표현

### softmax()

* softmax() vs sigmoid()
  * sigmoid() : 함수 **각각의 출력값이 0 ~ 1 사이 값**을 가짐
  * softmax() : **전체 출력값의 합이 1**이되어야 하기 때문에 학습효과가 증가

![](C:\Users\samsung\Desktop\softmaxformula.PNG)

![](C:\Users\samsung\Desktop\graphsigsoft.PNG)



#### Categorical Cross-Entropy Error(CEE)

* CEE = -sum(y * log(y_hat))

---

## Error Backpropagation

> Backpropagation : 역전파

### Forward Propagation

* 함수형 Model 의 학습원리
  * Gradient Descent(경사하강법)
  * w = w - r(학습률) * dw(w의 미분 : 경사값 --> 시간이 오래걸림)

* 시간이 오래걸리는 것을 없애고 싶음
  * **수치미분 과정없이 미분값을 획득**



* 각 학습 단계의 Parameter Update를 위해서 Parameter별 **편미분값**필요
  * Gradient Descent
  * 만약 Parameter 개수가 100만개 이상이면 수치 미분이 가능한가?
    * **많은 컴퓨팅 자원과 시간 소요**

* Parameter 개수는 Model Capacity에 영향을 준다.
  * Parameter의 개수가 증가하면, Model Capacity가 좋아지지만, **학습시간에 부정적 영향**

---

#### Chain Rule

* 신경망 모델은 Node(Function)들의 연결
  * Neural Network 는 **간단한 함수들이 중첩**으로 구성
  * 각각의 layer를 거치면서 sigmoid() 함수에 겹쳐지는 합성(중첩) 함수의 형태로 나타나게 됨.
* Chain Rule
  * y_hat = sigmoid(W3 * sigmoid(W2 * sigmoid(W1X + b1)+ b2) + b3)
  * Input(X) -> f1(#) -> f2(#) -> f3(#) -> Output(y_hat)

* 미분의 연쇄법칙
  * 합성함수 미분 : 함성함수를 구성하는 **개별 함수 미분의 곱**

---

#### Backpropagation Algorithm

* Forward propagation을 수행하여 y_hat을 계산
  * y 와 y_hat을 사용하여 **오차값**계산
* 학습 : 오차값이 감소하는 방향으로 weight 수정
  * 효율적은 경사값(Gradient) 계산을 위해 Backpropagation 수행
  * Parameter Update를 위해 **출력층의 오차값을 은닉층으로 전달**
* **미분의 연쇄법칙 + 오차 역전파 알고리즘**
  * **수치미분과정없이 학습을 위한 경사값 계산**
  * 빠른 속도로 학습 가능
* 전방향 연산에서 계산된 값을 재사용
* 전방향 연산에서 계산된 오차값(Error)을 전달



#### 오차값 * 출력값(1 - 출력값) * 입력값

* Forward propagation 결과들의 조합 패턴
* 오차값 : 뒤로부터 전달
* 출력값(1- 출력값), 입력값 : 전방향 연산시 계산한 값 재사용

> ppt , 실습 참고

---

### Vanishing Gradient

* Gradient
  * Parameter 학습을 위한 미분값
  * w = w - r * dw(Gridient값)
* Vanishing
  * **0**이 된다는 의미
* Layer를 깊게 쌓으면 , 중첩함수가 더 많아져서 곱해지는 것이 더 많아진다.
  * sigmoid 미분값이 계속 곱해짐
  * sigmoid 함수의 미분하면 최대치가 **0.25**로 1보다 작은 값 생성
  * 계속 곱해지다 보면 **Gradient값이 0으로 가까워져 미분값(기울기) 가 0이되는 문제 발생**
* Activation Function(sigmoid) 을 **다른 함수로 대체**하여 학습

![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile2.uf.tistory.com%2Fimage%2F997E1B4C5BB6EAF239A91B)

> *source : https://excelsior-cjh.tistory.com/177*

![](https://www.researchgate.net/publication/317679065/figure/fig10/AS:654765507768342@1533119670534/5-Activation-functions-in-comparison-Red-curves-stand-for-respectively-sigmoid.png)

> *source : https://www.researchgate.net/figure/5-Activation-functions-in-comparison-Red-curves-stand-for-respectively-sigmoid_fig10_317679065*

> activation function : google

---

### Optimization Method : 최적화 기법

> *source :http://shuuki4.github.io/deep%20learning/2016/05/20/Gradient-Descent-Algorithm-Overview.html*

| Optimization Method              |                  |
| -------------------------------- | ---------------- |
| Stochastic Gradient Descent(SGD) | SGD              |
| Momentum                         | Momentum         |
| Nesterov Momentum                | Momentum         |
| Adaptive Gradient(Adagrad)       | Adagrad          |
| RMSProp                          | Adagrad          |
| Adam(Adaptive Moment Estimation) | Adagrad,Momentum |
| AdaDelta                         | Adagrad,Momentum |



#### Stochastic Gradient Descent(SGD)

> Stochastic : 확률적

* 전체 데이터(batch) 대신 **일부 데이터**(mini - batch)를 사용

  * ex) 10000개의 data가 있으면, 전체 데이터를 한꺼번에 따 쓰는 것이 아니라,

    ​       구간을 나눠, 예를 들어 1000개씩 10번 하는 경우가 SGD

* batch GD보다 부정확할 수 있지만 계산 속도가 훨씬 빠름

* 같은 시간에 더 많은 step 이동 가능

* 일반적으로 batch의 결과에 수렴한다.

* W(t+1) = W(t) - Y * dE
  
  * 경사하강 공식 자체가 바뀌지 않는다.



#### Momentum

* 이동과정에 **관성**을 기억해 방향이 급격하게 꺾이는 것을 방지하기 위함

* 현재 이동하는 방향과 별개로 **과거 이동 방향을 기억**하여 이동에 반영
* 이전 가중치의 업데이터양과 방향이 크게 변화하지 않도록 조정
  * 바로 **직전 시점의 가중치**업데이터 변화량을 적용
  * 바로 직전의 가중치를 더해주는 방식

![](C:\Users\samsung\Desktop\momentum.PNG)

#### Adaptive Gradient(Adagrad)

* 학습률(Learning Rate) 이 작으면 안정적이지만 학습 속도는 느려짐

* 학습 횟수가 증가함에 따라 **학습률을 조정**하는 옵션 추가

* 학습률 감쇠식 추가

* 학습률은 처음에는 컷다가, 학습하는 횟수가 늘어남에 따라 점점 작아지는 것이 

  최소값으로 가까이 가기에 유리하다.

  ex) 목표지점으로 가까이 가기 위해서, 처음에는 보폭을 크게 가다가, 목표지점에 다가갈수록

  ​       보폭을 줄이는 것과 같다고 생각하면 쉬움

![](C:\Users\samsung\Desktop\adaptive.PNG)

#### Root MEAN Square Propagation(RMSProp)

* Adaptive 방식
* Adagrad의 단점인 Gradient **제곱합을 지수평균으로 대체**

#### Adaptive Moment Estimation(Adam)

* RMSProp 과 Momentum 방식의 **장점을 합친**알고리즘
* Momentum과 같이 지금까지 계산해온 기울기의 지수평균을 저장
* RMSProp과 같이 기울기 제곱값의 지수평균을 저장

---

