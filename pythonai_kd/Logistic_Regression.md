# Logistic Regression

### Encoding

* **Integer Encoding**

  ```python
  from sklearn.preprocessing import LabelEncoder
  ```

  * 문자형 변수 --> 숫자형 변수 변경
  * ex) 'europe' : 0 , 'korea' : 1 , 'usa' : 2

* **One-Hot Encoding**

  ```python
  from sklearn.preprocessing import OneHotEncoder
  ```

  * 하나의 값만 True(1) , 나머지 False(0)

---

### Classification(분류)

* 이진(Binary)
  * **0 or 1** 로 분류
  * ex) 구매고객  : 남자? 여자?, 물건 : 정상? 불량?, 코로나 검사 : 양성? 음성?
* 다중(Categorical)

---

### Sigmoid

![](https://upload.wikimedia.org/wikipedia/commons/5/53/Sigmoid-function-2.svg)

* 데이터를 두 개의 (0,1) 사이로 바꾸는 기본적으로 이진분류 형태를 띄게 만든다.

#### Classification(범주예측) 모델

* Output(y) 의 수치예측이 아닌 **어떤 범주에 속하는지에 대한 예측**(확률) 모델링
* Regression(수치예측) 모델에 **Sigmoid() 필터**를 적용하여 구현
  * 일반적으로 분류기준을 0.5로 지정(변경가능)
  * 0.5보다 크면 1, 0.5보다 작으면 0으로 분류
* **신뢰도 검증**(Model Validation) 이 필요함
  * Confusion Matrix , Accuracy, Precision, Recall
* sigmoid(wx+b) 함수에서 w는 기울기 , b는 좌우이동

> sigmoid , google drive gif 참고

---

#### Cross-Entropy Error(CEE)

* 서로 **다른 사건의 확률** 을 곱하여 Entropy를 계산
  * y : 실제값 , y_hat : 예측값
* y를 Cross-Entropy 의 가중치로 적용(이진분류 : 0 or 1)
* Binary Cross-Entropy Error = -y * log(y_hat) - (1-y) * log(1- y_hat)

![](C:\Users\samsung\Desktop\cee.PNG)



### 이진분류

#### Binary Confusion Matrix

![](https://upload.wikimedia.org/wikipedia/commons/3/32/Binary_confusion_matrix.jpg)

* 실제(y) : Actual class
* 예측값(y_hat) : Predicted class

#### Entropy(불확실성 척도)

* 불확실성의 정도
* 확률변수의 평균 정보량(기댓값)
* 불확실성(Entropy)이 낮으면 분류정확도가 높아짐

![](data:image/png;base64,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)

#### Confusion Matrix

![](https://upload.wikimedia.org/wikipedia/commons/a/a1/ConfusionMatrixRedBlue.png)

---

### Business Impact (어떤일에 부정적 영향?)

#### 정확도 (Accuracy)

* Positive 와 Negative 로 맞게 분류된 데이터의 비율
* (TP + TN) / (TP + TN + FP + FN)



#### 정밀도 (Precision)

* Positive로 분류된 결과 중에서 실제 Positive 의 비율
* **Negative를 Positive로 틀리게 분류 시** 문제 발생 : 스팸메일 필터링
* TP / (TP + FP)



#### 재현율 (Recall)

* 실제 Positive 중에서 Positive 로 분류된 비율
* **Positive를 Negative로 틀리게 분류 시** 문제 발생 : 코로나 진단
* TP / (TP + FN)

![](C:\Users\samsung\Desktop\kd\tp.PNG)

---

