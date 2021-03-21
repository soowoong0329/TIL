# Overfitting Issues

* Train 데이터에만 최적화 된 상태

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/overfitting.PNG?raw=true)

### Train Loss VS Validation Loss

1. **더 많은 Train Data**
   
   * 실제로 성능이 좋아질까? ==> **좋아질 수 있다.**
2. **Model Capacity**
   * Capacity에 영향을 주는 것은 Parameter
   * **Model 스펙이 너무 높아서 과적합이 나타날 수 있다.**
     * Parameter 개수를 줄이면 성능이 좋아질 것이다.
     * **Hidden Layer 및 Node 개수 줄이기**

3. **L2 Regularization**

   * 학습에 영향

   * 가중치의 제곱(L2 = ridge)에 비례하는 노이즈를 Cost Function에 추가
   * 가중치 감소: Weight Decay
   * L1 or lastic 둘 다 가능(Regularization 실습 참고)

   > DNN_mnist_Categorical

   * Model Capacity 줄이면서 L2까지 주는 것도 가능하다.

4. **Dropout**

   * 훈련과정에서 네트워크 일부 출력 특성의 연결을 무작위로 제외 시킴

![](https://miro.medium.com/max/1200/1*iWQzxhVlvadk6VAJjsgXgg.png)

> *source : https://medium.com/@amarbudhiraja/https-medium-com-amarbudhiraja-learning-less-to-learn-better-dropout-in-deep-machine-learning-74334da4bfc5*

5. **Batch Normalization**

   * 활성화 함수의 입력값을 정규화 과정을 수행하여 전달

   * Gradient Vanishing 문제 해결 , 더 큰 Learning Rate 사용 가능

   * Input Data(x) : 정규분포 형태로 들어와서 노드를 지나면서,

     WX + b로 분포가 변할 수 있다.

     * 분포가 치우치거나, 변할 수 있는데, 이걸 중간중간에 **Batch Normalization**으로 정규분포 형태로

       만들어서 다음 노드로 전달하여 정규화 과정을 수행한다.

![](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile9.uf.tistory.com%2Fimage%2F99BFAE495BBE005924EA2D)

> *source : https://excelsior-cjh.tistory.com/178*

---

> DNN_mnist_categorical, Fashion_mnist, overfitting

