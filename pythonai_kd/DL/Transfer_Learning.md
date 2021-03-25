# 전이학습 (Transfer Learning)

* Learning :  Parameter Update

* **누군가 만들어놓은 parameter를 가지고 우리가 원하는 분류를 할 수 있을까? == 전이학습**

#### ILSVC(ImageNet Large Scale Visual Challenge)

* 1000가지 이미지 클래스를 분류(Classification)하는 문제
* 딥러닝 기반의 parameter model이 좋은 성능을 보여주고 있음

#### 사전 학습된 parameter(Model)을 가져와서 적용하자 :heavy_exclamation_mark:

* 고려사항

  * **Input shape를 맞춰줘야한다.**

    * ex) (150,150,3)인 이미지를 분류하고 싶은데, 생성된 모델은 Input shape이 다를 수 있다.

  * **끝 쪽에 Classification Dense Layer 재사용이 불가능 할 가능성이 크다.**
    * 1000가지 분류하는 모델이기 때문에, 이진분류(sigmoid), 10개 분류(softmax) 등 사용 불가능

      고쳐줘야 한다.

* **학습된 parameter를 통해 

---

#### LeNet

* 얀 르쿤(Yann Lecun) 연구팀에서 개발한 최초의 CNN 구조
* 합성곱(Convolution), Subsampling(Max Pooling), Full Connection(Classification)

![](https://hoya012.github.io/assets/img/image_classification_guidebook/1.PNG)

> *source : https://hoya012.github.io/assets/img/image_classification_guidebook/1.PNG*

#### AlexNet

* 2012 ILSVC 대회 우승
* LeNet과 유사한 구조이며, **2개의 GPU**로 병렬 연산 수행

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99FEB93C5C80B5192E" style="zoom: 80%;" />

> *source :https://bskyvision.com/m/421*

#### GoogLeNet(InceptionNet)

* 2014 ILSVC 우승
* Inception Module : 총 9개의 가로 방향으로 깊은 구조

![](https://miro.medium.com/max/700/0*rbWRzjKvoGt9W3Mf.png)



#### ResNet

* 2015 ILSVC 우승
* GoogleNet의 약 7배dls 152 Layers로 구성
* Layer가 깊어져 학습이 안되는 문제(Vanishing Gradient)를 **Skip Connection**을 통해 해결

![](C:\Users\samsung\Desktop\resnet.PNG)

---

### VGGNet

* **Layer 개수에 따라 VGG16과 VGG19** 두 가지 모델로 구성

* 요즘 많이 사용

![](https://ichi.pro/assets/images/max/724/1*4F-9zrU07yhwj6gChX_q-Q.png)

> *source : https://ichi.pro/assets/images/max/724/1*4F-9zrU07yhwj6gChX_q-Q.png



> google : CNN_Feature_extraction



#### Feature Extraction

* 사전에 학습된 모델을 사용하여 특성 추출
  *  Feature Extraction : Parameter 재사용
  * Classification : Parameter학습(기존에 것 사용불가, 우리에 데이터에 맞는 새로운 parameter 로 학습)

![](C:\Users\samsung\Desktop\feature extraction.PNG)



#### Fine Tuning 

