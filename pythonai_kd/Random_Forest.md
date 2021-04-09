# Random Forest(Ensemble)

1. 나무가 여러개
2. 다양한 모양으로 생성

* 원본 Data의 특징을 포함하는 형태로 재구성
  * 사람의 의도가 반영되지 않는 형태로 random하게 
  * 원본데이터의 특징을 포함하는 형태로 재구성해야한다.

* **덜 정확한 분류모델** 여러개를 모아서 더 정확한 분류 모델을 만들 수 있을까?
  * 반드시 그런 것은 아니지만, Train data는 원본 데이터보다 개수가 적다.
  * data의 수가 많을 수록 결과가 좋아진다.
  * train data가 개수가 적기 때문에 model이 덜 정확한 분류모델이 된다.
* 앙상블(Ensemble) : 여러가지 모델을 사용하여 **정확도를 개선**하는 방법



* 랜덤 포레스트  : 의사결정나무만의 앙상블(Ensemble)
  * 다수의 의사결정 나무들의 결과로부터 모델을 생성
  * 모델 생성에 다양성(Diversity)과 임의성(Random)을 부여
  * 모델 정확도를 높이고 과적합 발생 가능성을 낮춤
  * 올바른 예측은 강화하고, 잘못된 예측은 상쇄하는 경향 존재
    * Boosting 계열의 모델들이 이러한 경향을 보임

---

### 다양성(Diversity)

#### 배깅(Bagging)

* Bagging = Bootstrap(다양한 모델 생성) + Aggregating(다양한 결과 취합)
* 주어진 Data를 사용하여 여러 개의 서로 다른 Train Data를 생성
  * 생성된 Train Data마다 별도의 의사결정 나무 모델 생성
  * Hyperprarameter(n_estimators)로 의사결정 나무 개수 지정
* 개별 Train Data 는 Booststrap 방식으로 생성
  * Bootstrap Data는 Original Data에서 단순 복원 임의추출법으로 생성
    * data가 중복 될 수도 누락될 수도 있다.
* 여러 개의 Bootstrap 모델의 결과를 통합
* 분류 모델 : 다수결 또는 가중치를 적용하여 통합
* 예측모델 : 평균값 또는 가중 평균값으로 통합





### 임의성(Random) - Random Subspace

* 의사결정 나무 생성이 변수 무작위 선택(비복원 추출)
* 원래 변수에서 무작위로 입력 변수를 추출하여 적용
* 무작위 입력 변수의 개수를 1 ~ 전체 변수의 개수 사이에서 지정
* Hyperparameter : max_features
  * 기본값 : sqrt(변수의 개수) : ex) 변수 9개 = 3개선택(max_features = 3)

---

### Cross Validation

* Overfitting을 방지하기 위하여 수행
* Validation을 한번만 수행하면 특정 Data에만 최적화 될 수도 있다!
* 다양하게 Train Data와 Validation Data를 변경하면서 모델 평가를 수행
* Training Data 를 무작위로 균등하게 K개의 그룹으로 나누어서 검증
* (K-1) 개 training Fold 와 1개의 Validation Fold를 지정
* K는 Hyperparameter
* 일반적으로 K값은 5 ~ 10 정도로 선택
* K개의 결과의 평균을 Validation Data에 적용하여 평가
* Data가 충분히 많다면 K- Fold Cross Validation 수행
* 데이터가 매우 적다면 데이터의 개수만큼 교차 검증 수행

* 시간오래걸림

---

### Boosting

* Random Forest : 병렬처리가 가능하다.
  * 나무를 한꺼번에 여러개를 만들수 있다.
  * Bootstrap된 Data를 통해서 나무를 여러 형태로 만들 수 있음.

#### Boosting

* **순차적처리**하면서 학습이 반복될수록 모델이 좋아진다.
* 원본 Data에서 Bootstrap Data를 뽑아서 나무를 만든 뒤 성능평가
  * 성능평가 한 Error가 나오면 어느 정도 보완시켜서 2번 째 Bootstrap Data sampling 함
  * 어느정도 오차를 반영할 것인지는 Learning Rate(학습률)로 결정
* **순차적으로 처리**하기 때문에 Random Forest보다 느리다.

* 순차적으로 boosting하면서 처리하기 때문에 나무가 많을수록 좋아진다.(일반적, 무한대로 좋아지는 것은 아님)