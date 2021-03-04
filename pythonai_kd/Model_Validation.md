# Model Validation :100:

> Model을 사용해서 Data의 분포를 설명/표현

#### Validation(검증)

* 우리가 만든 모델이 **사용에 적합한가?** 확인하는 작업



#### Model Capacity

* **Model의 Data에 대한 설명력**
* Parameter의 개수가 직접적으로 Capacity에 영향을 준다.
* Parameter 개수가 많아지면 설명력이 좋아진다고 생각할 수 있다.(무조건은 아님)

---

### Data Analytics vs Machine Learning

* Data Analytics
  * 단순히 **과거 행동의 특징**을 확인(EDA)
  * 과거 행동의 특징을 파악해서 **미래 행동의 결과 예측**(prediction)



* Machine Learning
  * Model 과거 행동의 특징을(parameters) 학습

---

#### Training Error

* 기본적으로 학습은 **Training Error**를 **최소화**하는 방향으로 진행

* Training Data에 Model을 적용하여 확인한 실제값과 예측값의 차이(오차)

* $$
  mean((y- \hat y)^2)
  $$

* 여러 개의 Model을 생성 후 각각의 Training Error(MSE)를 비교



#### Overfitting (과적합)

* 학습한 결과가 training data에만 최적화된 모델을 생성
  * 모델 생성 시 활용하지 않은 data에서 성능이 급격히 낮아짐

---

#### Generalization Error

* 예측이나 분류할 때 Data에 적용 했을 때 발생하는 에러
* 현실적으로 측정 불가능
  * Generalization Erro 추정을 위하여 **Testing Error**를 사용한다.



#### Testing Error

* 모델 학습 후 반드시 평가가 필요
* Training Data : 학습을 위해 제공되는 데이터
* Testing Data : 학습결과를 평가 하기 위한 데이터

---

#### Machine Learning / Deep Learning

* Modeling 목적
  * 일반화된 Model을 만드는(학습시키는) 것
  * Model 생성(학습) 시 사용되지 않은 data에서도 유사한 성능을 제공할 수 있어야 한다.
  * training error 와 test error(MSE)가 gap이 크면 안된다.(일반화된 모델의 목적)
    * == overfitting(과적합) 되지 않았다고 말할 수 있다.

### Validation Approach

: 미래에 만나는 **에러를 추정**해보기 위해 사용

: Train Data로 모델 만들어서 ,Validation Data로 성능평가하고, 최적의 모델을 찾아 Test Data는 **한번만 사용**하기 위해

: Generalization(일반화) Error를 찾아내기 위해



#### Testing Error

* Testing Data에 최적 Model을 적용하여 얻은 실제값과 예측값의 차이(오차)
* Testing Error를 사용하여 실무 데이터에 대한 Generalization Error를 추정
* Training Data를 Training Data와 Validation Data로 분리하여 모델을 평가

---

