# Pandas II

## Data Preprocessing :new: (데이터 전처리)

* Pandas DataFrame : **집단의 특징을 확인** 하기위한 작업

## Missing Value : 결측치 처리

### **데이터의 특징에 영향을 주지 않도록** 결측치 처리가 중요 !

#### 결측치(NA,NaN,NULL)

* 결측치가 존재하면 Dataframe의 올바른 특징을 확인 할 수 없다.
* 연산(평균,분산,...) 이 불가능하다.

#### 결측치 처리

1. 삭제(제거) : 결측치를 삭제했을 때 원하는 특징인가? : **정확성에 문제**가 생길 수 있다 !
   * 행 삭제
   * 열삭제

2. 대체
   * 직접 올바른 값을 채워 넣는 것이 가장 BEST :thumbsup: (현실적으로 불가능)
   * 분석하는 사람의 **의사결정**에 따라 대체 값이 달라진다.
     * 수치 : 평균(일반적으로 평균으로 대체 , 정답은 아님), 중앙값 ...
     * 문자 : 최빈값(일반적 , 정답은 X)

---

> titanic dataset 활용

* 데이터셋 확인

```python
import seaborn as sns
DF = sns.load_dataset('titanic')

DF.head(10)
```

```python
DF.shape()
```

```python
DF.info()
```

* 결측치 확인

```python
DF['deck'].value_counts(dropna = False) # dropna = False : 결측치 출력
```

![](C:\Users\samsung\Desktop\dropnafalse.PNG)

* `.isnull()` : 결측치를 'True' 로 출력

```python
DF.head(10).isnull()
```

![](C:\Users\samsung\Desktop\isnull.PNG)

* 각 Column 별로 결측치 개수 확인

![](C:\Users\samsung\Desktop\axis.PNG)

```python
DF.isnull().sum(axis=0)
```

* `.notnull()` : 결측치를 'False'로 출력

```python
DF.head(10).notnull()
```

![](C:\Users\samsung\Desktop\notnull.PNG)

* 결측치가 300개 이상인 열 삭제

```python
DF.dropna(thresh = 300, axis = 1).shape
```

* 결측치가 하나라도 있는 행 삭제

```python
DF.dropna(subset = ['age'], how = 'any', axis = 0).shape
```

---

#### 결측치 치환

* 연속형 데이터 치환
  * ex) 'age'의 결측치를 평균값으로 치환

```python
DF['age'].head(10)
```

![](C:\Users\samsung\Desktop\agebefore.PNG)

```python
DF['age'].fillna(int(DF['age'].mean(axis=0, inplace = True)))
```

* `inplace = True`
  * 원래 DataFrame에 결측치를 치환함(원래 DataFrame에서 결측치가 없어짐)

![](C:\Users\samsung\Desktop\ageafter.PNG)

* 명목형 데이터 치환
  * ex) 'embark_town'의 결측치를 최빈값으로 치환

```python
DF['embark_town'][825:830]
```

![](C:\Users\samsung\Desktop\embarkbf.PNG)

* 최빈값 확인하기

```python
![fillbf](C:\Users\samsung\Desktop\fillbf.PNG)most_freq = DF['embark_town'].value_counts(dropna = True).idmax()

most_freq

### 'Southhampton'
```

* 치환

```python
DF['embark_town'].fillna(most_freq, inplace = True)

DF['embark_town'][825:830]
```

![](C:\Users\samsung\Desktop\embarkaf.PNG)

* 이전 데이터포인트로 치환하기

```python
DF = sns.load_dataset('titanic')

DF['embark_town'][828:831]
```

![]()![fillbf](C:\Users\samsung\Desktop\fillbf.PNG)

```python
DF['embark_town'].fillna(mathod='ffill',inplace = True) #ffill : 이전(forward) 데이터포인트로 치환
# 앞이 결측치이면 그 앞, 결측치가 없을때까지 이동해서 치환

DF['embark_town'][828:831]
```

![](C:\Users\samsung\Desktop\ffill.PNG)

* 다음 데이터포인트로 치환

```python
DF = sns.load_dataset('titanic')
DF['embark_town'][828:831]
```

```python
DF['embark_town'].fillna(method='bfill', inplace = True) # back
DF['embark_town'][828:831]
```

![](C:\Users\samsung\Desktop\bfill.PNG)

---

