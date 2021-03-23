p. 132 항상 기억하고 정리하기

DNN은 결국 Hyper Parameter 들을 어떻게 넣어서 모델의 성능을 향상 시킬 것인가? 가장 중요

---

# Convolutional Neural Network : CNN

> 주로 이미지 분류에 사용하지만, 예측이나 다른 분류문제에도 사용할 수 있다.

#### Convolutional (합성곱) 신경망 알고리즘

* 이미지처리에 주로 사용
* **합성곱 연산을 이용하여 가중치의 수를 줄이고 연산량을 감소**
  * 가중치의 수를 줄인다?
  * Parameter수를 줄인다 == Model의 Capacity를 줄인다.
* 여러 개의 **Filter(Parameter matrix)**로 이미지 특징(Feature Map) 추출
* 말단에 Sigmoid 또는 Softmax 함수(DNN)를 적용하여 이미지 분류작업 수행

* LeNet, AlexNet,VGGNet,InceptionNet,ResNet등 이미 만들어진 CNN 모델등이 존재
  * 이미 만들어진 Model이 성능이 좋은 경우가 많다.

---

### CNN - Hyperparameter

#### Filter

![](C:\Users\samsung\Desktop\cnnfilter.PNG)

* Filter를 Input_Data에 적용하여 **특징 맵(Feature Map)** 생성

* Filter값은 Input_Data의 특징을 학습하는 가중치(Weight) 행렬

* 동일한 Filter로 Input_Data전체에 **합성곱 연산(Convolutional)** 적용

![](http://deeplearning.stanford.edu/wiki/images/6/6c/Convolution_schematic.gif)

> *source : http://deeplearning.stanford.edu/wiki/images/6/6c/Convolution_schematic.gif*



#### Stride

<img src="https://taewanmerepo.github.io/2018/01/cnn/filter.jpg" style="zoom: 33%;" />

> *source : http://taewan.kim/post/cnn/*

* Filter를 적용하기 위해 **이동**하는 위치의 **간격**
* Stride값이 커지면 출력 특징 맵의 크기 감소



#### Pooling

<img src="https://taewanmerepo.github.io/2018/02/cnn/maxpulling.png" style="zoom: 33%;" />

> *source : http://taewan.kim/post/cnn/*

* 가로 및 세로 방향으로 크기를 줄이는 연산
* Pooling window 및 Stride값 지정

* Average Pooling 보단 주로 Max Pooling 사용



#### Padding

<img src="https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile22.uf.tistory.com%2Fimage%2F9916C23F5BC97EEE31EF65" style="zoom:80%;" />

* Padding은 **출력 크기를 조정** 목적으로 사용
* 합성곱 연산을 수행하기 전에 Input_Data주변을 0으로 채우는 것
* Layer가 깊어질수록 Input_Data가 계속 잘려나가 , 없어질 수 있음
  * Layer가 깊어지면서 Input_data가 잘리지 않도록 Padding사용



#### Channel

<img src="https://kjh107704.github.io/assets/img/postImg/2020-07-06-14-47-50.png" style="zoom:67%;" />

* n차원 데이터 : **n차원 Filter**를 사용하여 합성곱 연산 수행
* Input_Data의 채널 수와 Filter의 채널 수는 같아야함
  * Tensorflow 에서 channel은 자동으로 맞춰짐

> *source : https://kjh107704.github.io/posts/DL-CNN-3/*

#### Classification

* CNN 마지막 단계에서 분류를 위한 필터를 적용
  * 이진분류(Binary) : sigmoid ( 0 or 1)
  * 다중분류(Categorical) : softmax

#### Convolusion을 거치면서 Feature Map 한(one) 픽셀이 가지는 함축적으로 학습한 특징이 많아진다.(=한 픽셀이 포함하고 있는 이미지의 범위가 넓어진다.)

![](C:\Users\samsung\Desktop\cnnclassification.PNG)

> *source : https://hunkim.github.io/ml/lab11.pdf*

---

> Google Drive : ALL CNN

