# Decision Tree :palm_tree:

* 가능한 대답이 두가지인 **이진질의(Binary Question)**의 **분류 규칙**을 바탕으로 최상위 루트 노드의 질의 결과에 따라 가지(Branch)를 타고 이동하며 최종적으로 분류 또는 예측값을 나타내는 리프(Leaf)까지 도달

* 범주형 자료 : classification tree(분류 나무)
* 수치형 자료 : regression tree(예측 나무)

![](https://github.com/soowoong0329/TIL/blob/master/img/decisiontree.PNG?raw=true)

| Decision Tree |                                                      |
| ------------- | ---------------------------------------------------- |
| Root Node     | 최상위 노드                                          |
| Splitting     | 하위 노드로 분리 되는 것(불순도가 낮아지는 방향으로) |
| Branch        | 노드들의 연결(의사결정 나무 일부분)                  |
| Decision Node | 2개의 하위 노드로 분리되는 노드                      |
| Parent Node   | 분리가 발생하는 노드                                 |
| Leaf          | 더 이상 분리되지 않는 최하위 노드                    |
| Child Node    | 분리가 발생한 후 하위 노드                           |

* 규칙 기반으로 **직관적으로 이해**하기 쉽고 설명력이 좋은 알고리즘
  * 각 노드별로 **불순도**에 기반하여 최적의 분류 규칙을 적용한다.
  * 각 리프는 동질성이 높은 적은 수의 데이터 포인터를 포함한다.



* 너무 **복잡하고 큰 의사결정 나무 모델**은 Model 의 Capacity가 높아져 과적합 문제가 발생한다.
  * Pruning : 가지치기
  * `max_depth` , `min_samples_leaf` 등으로 대응

---

### Machine Learning Modeling

#### I. Regression

* Learning --> MSE(Train) : mean(y - y_hat)^2 : 실제값과 예측값의 차이 
* Validation --> MSE(Test) : mean(y - y_hat)^2 : 실제값과 예측값의 차이

#### II. Classification(Binary)

* Learning --> MSE(가능은 함) , CEE
* Validation --> Accuracy, Precision, Recall score (F1 - Score : Precision + Recall)



#### 정보이득량

* **자주 발생하지 않는 사건은 자주 발생하는 사건보다 전달하는 정보의 양이 많다.**

* Degree of Surprise(놀람의 정도)
  * 예상하기 어려운 정보에 더 높은 가치를 매기는 것

### Entropy(불순도의 척도 : Metric)

* **불순도를 수치화한 지표**
* **정보량의 기댓값**
  * Entropy = E(-log(P(x)))
  * 놀람의 평균 정도
* **Entropy가 낮으면 분류정확도가 높아진다.**

![](https://upload.wikimedia.org/wikipedia/commons/2/22/Binary_entropy_plot.svg)

> formula in ppt 150.



### Gini Impurity Index

* 데이터의 통계적 분산정도를 정량화하여 표현한 값이다.

* **특징 지니 지수가 클수록** 불순도가 낮다.
  * 지니지수가 작은 특징으로 의사결정 나무의 노드를 분리
* 두 개로 분리된 각 노드의 지니 지수를 계산

![](https://i.stack.imgur.com/E7Fak.png)

> gini in ppt 153.

---

