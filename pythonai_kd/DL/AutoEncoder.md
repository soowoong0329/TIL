# AutoEncoder

* **Auto Encoder 목적 : Latent Space를 학습하는 것**
  * Latent Space(잠재 공간) :  관측 데이터를 잘 설명할 수 있는 공간(Manifold)
  * 잠재공간을 알 수 없음(추정만 가능)
* 차원축소 : 관찰 데이터 기반의 잠재 공간을 파악하는 것

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTTzpo80GCm7slaBpgocnLXEp7g21hjpbfrpQ&usqp=CAU)

> *source : https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTTzpo80GCm7slaBpgocnLXEp7g21hjpbfrpQ&usqp=CAU*

* 위 사진 처럼 6개 숫자로 잠재공간 추정
  * 6개의 숫자(Vector)로 표현
  * 6개 숫자로 encoding 한 것
    * 크게하거나, 작게하거나 가능

---

![](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F996C93475BDC97C00A)

> *source : https://excelsior-cjh.tistory.com/187*

* **인코더** : 인지 네트워크로 입력을 **내부 표현**으로 변환
  * 고차원의 정보를 저차원의 정보로 축소 시키는 것

* **디코더** : 생성 네트워크로 **내부 표현**을 출력으로 변환
* 입력 데이터(x) 와 출력 데이터(x) 가 같음
  * Hidden Layer의 개수를 줄여 제약을 준다.
    * 입력 데이터의 축소, 압축효과
    * **주성분분석(PCA)**으로 구현 가능

---

### Variational AutoEncoder : VAE

* 잠재공간의 값(개념 벡터)을 **가우시안 확률분포의 값(정규분포) 범위**로 제공

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/vae1.PNG?raw=true)

* VAE는 입력 이미지가 통계적 과정을 통하여 생성되었다고 가정
  * 이미지를 2개의 벡터 z_mean과 z_log_var로 매핑(평균,분산)
  * 이 벡터는 잠재 공간 상 확률분포를 정의하고 디코딩을 위한 포인트 샘플링에 사용

![](https://i.stack.imgur.com/49HNA.png)

> *source : https://stats.stackexchange.com/questions/423758/variational-autoencoder-understanding-this-diagram*

* 잠재 공간의 정규분포에서 z값을 무작위 샘플링하여 디코더로 복원

* **Auto Encoder는 생성모델이 아니기 때문에 input값과 output값을 같게 decoding하고 싶은것**

  * Auto Encoder의 잠재공간은 고정된 값

* **VAE는 생성모델**이기 때문에 잠재 공간이 고정되어 있지 않고, 똑같은 값이 아니라, 다른 값을 뽑아내어

  기존의 것이 아니라, **비슷하게 생긴 다른 output을 생성하고 싶은 것**

  * **input과 상당히 유사하지만, 실질적으로 다른 output생성**

  * Sample Vector를 통해서 새로운 output 생성 가능

    * ex) 눈만 키우거나(눈 vector를 뽑아내 다른 vector를 두고 눈 vector만 조정),

      ​       얼굴 축소사진(같은 원리)

* VAE는 구조적이고 연속적인 잠재 공간 표현을 생성

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/vae2.PNG?raw=true)

---

> google drive : Variational_AutoEncoder



