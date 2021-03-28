# Multi - Layer Perceptron

## Neural Network 

> 함수형모델 : Input, Output / x,y

* 인공 신경망(Artificial Neural Network) : ANN
  * **머신러닝** 분야에서 연구되는 **학습 알고리즘**
    * 최적의 w,b를 update
  * 수치예측, 범주예측, 패턴인식, 제어분야에 응용
* **인간의 뇌 구조**를 모방하여 만들어짐(신경세포 : Neuron)
  * 수상돌기(Dendrite) , 시냅스(Synapse) , 신경세포체(Soma), 축색(Axon)
  * 수상돌기 = 입력, 축색 = 출력
  * 시냅스 = 가중값(Weight)을 갖는 연결네트워크, 신경세포체 = 노드

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/neural.PNG?raw=true)

### Perceptron

* 인공신경망의 한 종류
* 가장 간단한 형태의 Forward Network
* 노드 입력값(Input, x)과 가중치(Weight, w) **곱**을 모두 합함 + bias(b)
  * 합한 값이 활성화함수(sigmoid())의 임계치(0.5) 보다 작으면 0 , 크면 1 출력

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/logicgates.PNG?raw=true)

> https://www.youtube.com/watch?v=tYxkIOTdeu8

* NAND
  * AND의 부정
  * AND와 반대의 결과
* XOR
  * Exclusive OR
  * 2개가 같으면 거짓
  * 2개가 다른 값이면 참

* y = WX + b 

> 대문자 == 행렬

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/logicgates2.PNG?raw=true)

* **XOR Multi Layer**

![](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F9974283B5AAE80D027B961)

> *source : https://gomguard.tistory.com/178*

---

#### Multi Layer Perceptron(MLP)

* 다중 Perceptron : 퍼셉트론으로 해결할 수 없는 비선형 분리 문제에 필요
* 여러 층(Layer)의 퍼셉트론을 쌓아서 동작(Input - Hidden - Output)
  * Single Layer보다 **Model의 Capacity가 높아져** , 더 어려운 데이터 처리 가능하다.
  * 선 하나하나가 Parameter,가중치(Weight) 라고 생각
  * hidden layer의 개수는 **Hyper parameter**
    * 해봐야 안다. (Decision Tree에서 깊이,나무수 같은 개념)

![](https://snappygoat.com/b/e2812ac9096827e98fc5c73f8ecd19f0fbc29099)

> *source : https://snappygoat.com/b/e2812ac9096827e98fc5c73f8ecd19f0fbc29099*

---

### Deep Neural Network(DNN)

![](https://www.kdnuggets.com/wp-content/uploads/deep-neural-network.jpg)

> *https://www.kdnuggets.com/2020/02/deep-neural-networks.html*

* Parameter 학습법 : Gradient Descent
  * 경사하강법을 사용해 W와 b를 학습
* Mulit Layer Perceptron 은 함수형 모델



#### ML / DL Modeling

* Model input 값 (x) 가 많아지면 Model의 Capacity가 좋아진다.
* Parameter(W,b) 값이 많아지면 Model의 Capacity가 좋아진다.
  * But !
    * Gradient Descent를 사용하기 때문에, 시간이 너무 오래걸림(Hardware적 문제)
    * 무작정 높이는 것은 Model에 부정적인 영향을 미칠 수도 있다. 

---

#### 미분

* 순간변화량 or 접선의 기울기
* 함수 : x(input) 와 y(output)의 관계
  * 입력변수(x) 가 변할 때, 함수 f(x)의 변화량
  * 함수 f(x),y 가 입력변수에 얼마나 민감하게 반응하는지?

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/lim.PNG?raw=true)

#### 편미분

* 입력변수가 2개 이상인 다변수 함수의 미분

* **변수 1개를 제외한 나머지 변수들은 상수로 취급 후 **

  **지정된 하나의** **변수에 대해서 미분 수행**



#### Chain Rule(연쇄법칙)

* 합성함수의 미분 -> 개별 함수의 미분의 곱

> google



#### 중앙미분

* 오차의 최소화 하기위해 사용한다.

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/centrallim.PNG?raw=true)

---

> google : tensorflow playground

