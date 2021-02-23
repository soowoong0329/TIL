# Data Structure :building_construction:

#### 데이터를 모아서 관리하는 방식

#### 데이터를 모아서 어떻게  관계를 설명할 것인가? (테이블구조, 트리구조, 네크워크 구조...)

#### Address / Index

* **Memory**(물리적 공간) 에 부여한 **Address**(논리적인) 구조

---

| 정형(Indexing,Slicing 가능) | 비정형               |
| --------------------------- | -------------------- |
| 문자열(String)              | 딕셔너리(Dictionary) |
| 리스트(List)                | Casting              |
| 튜플(Tuple)                 |                      |

---

# Python Packages :package:

## Numpy

* 수학 및 과학적 연산을 쉽고 빠르게 지원
* 다차원 행열(Array)을 효과적으로 처리

```python
import numpy as np
```

* Scalar-0D Array- Rank0 Tensor

```python
a0 = np.array(9)

print(a0)
```

* Vector - 1D Array - Rank 1 Tensor

```python
a1 = np.array([1,3,5,7,9])

print(a1)
```

* Matrix - 2D Array - Rank2 Tensor

```python
a2 = np.array([[1,2,3],
              [4,5,6],
              [7,8,9]])

print(a2)
```

* Array - 3D Array - Rank3 Tensor

```python
a3 = np.array([[[1,2],
               [3,4]],
              [[5,6],
              [7,8]],
              [[9,10],
              [11,12]]])

print(a3)
```

![](https://github.com/soowoong0329/TIL/blob/master//3_tensor.PNG?raw=true)

---

#### `shape()`

* 배열의 크기를 알려준다.

```python
AR = np.array([1,2,3,4,5,6,7,8,9,10,11,12])

print(AR)
```

> [1 2 3 4 5 6 7 8 9 10 11 12 ]

```python
AR.shape
>>> (12,)
```

* `.replace(행,열)`

```python
AR2 = AR.reshape(3,4)
```

```python
AR2.shape

### (3,4) # 3 X 4 행렬
```

* `.replace(축,행,렬)`

```python
AR3 = AR.reshape(3,2,2)
print(AR3)
###
"""
  [[[ 1 2]
	[ 3 4]
    
    [[ 5 6]
     [ 7 8]]
    
    [[ 9 10]
     [11 12]]] """
```

```python
AR3.shape

#### (3,2,2) : 3개 축(x,y,z) 를 가지는 2 X 2 행렬
```

* 10개 연속된 값 생성

```python
np.arange(10)
```

* 1 ~ 9 까지,1간격

```python
np.arange(1,10)
```

* 1 ~ 9 까지, 2간격

```python
np.arange(1,10,2)
```

* 생성된 Array에 `.reshpe()`사용 가능

```python
np.shape(1,10).reshape(3,3)
```

---

* 0과 1로만 구성된 Array(float 형태로 출력된다.)

```python
np.zeros(9)

### array([0.,0.,0.,0.,0.,0.,0.,0.,0.])
```

```python
np.ones(9)

### array([1.,1.,1.,1.,1.,1.,1.,1.,1.])
```

```python
np.zeros([3,4])

###
"""
array([0.,0.,0.,0.
      [0.,0.,0.,0.
      [0.,0.,0.,0.])
"""
```

* 단위행렬

```python
np.eye(3)
```

---

#### 난수 Array 생성

```python
np.random.rand(3,2,2)
```

* 난수 생성(비복원 추출 : 겹치는 문자로 출력된다.)

```python
# 1 ~ 45 숫자 중에 비복원 추출 5 X 6 행렬
np.random.randint(1,45, size = (5,6))
```

```python
np.random.seed(2045)
# 1 ~ 45 범위 숫자중에 5X6 행렬, 복원추출(replce=Flase)
np.random.choice(np.arange(1,46),size = (5,6), replace= False)
```

---

#### Array 연산

```python
a1 = np.array([1,3,5,7,9])
a2 = np.array([10,30,50,70,90])
```

```python
a1 + a2

### array([11,33,55,77,88])
```

```python
a2 - a1

### array([9,27,45,63,81])
```

```python
a2/a1

### array([10.,10.,10.,10.,10.])
```

```python
a1 * 3

### array([1,9,25,49,81])
```

#### 통계량 연산

```python
a1 = [1,3,5,7,9]
a2 = [10,30,50,70,90]
```

| 설명                | 함수           | 출력 결과               |
| ------------------- | -------------- | ----------------------- |
| 총합                | `a1.sum`       | 25                      |
| 평균                | `a2.mean()`    | 50.0                    |
| 분산                | `a2.var()`     | 800.0                   |
| 표준 편차           | `a2.std()`     | 28.284271247461902      |
| 최소값              | `a2.min()`     | 10                      |
| 최대값              | `a2.max()`     | 90                      |
| 누적(Cumulative) 합 | `a1.cumsum()`  | array([1,4,9,16,25])    |
| 누적(Cumulative) 곱 | `a1.cumprod()` | array([1,3,15,105,945]) |

#### Matrix 연산(행렬의 연산)

```python
A1 = np.array([2,4,6,8]).reshape(2,2)
print(A1)

A2 = np.array(3,5,7,9).reshape(2,2)
print(A2)
```

* A1 @ A2 : Matrix 곱

```python
A1.dot(A2)
###
"""
array([[ 36, 52],
	   [ 68, 100]])
"""
```

* A1 * A2 : 각각 값들이 곱해짐 (행렬 연산 X, Excel연산이라고 생각)

```python
A1 * A2
###
"""
array([[ 6, 20],
 	   [42, 72]])
"""
```

#### 전치 행렬

```python
np.transpose(A1)
###
"""
array([[2, 6],
	   [4, 8]])
"""
np.transpose(A2)
```

---



