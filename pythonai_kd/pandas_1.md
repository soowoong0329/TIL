# Python Packages :package:

## Pandas

* 데이터 처리&분석을 위한 파이썬 라이브러리
* 행,열로 구성
* 대용량 데이터처리에 유리하다.

```python
import pandas as pd
```

---

### Pandas - DataFrame

* 행,열이 존재하는 형태
* Array와는 다른 테이블 형태

```python
import pandas as pd

DF1 = pd.read_csv('파일이름.csv')
DF1
```

> CSV(Comma Seperate Value) : Excel에서 excelfile처럼 열어줌 , CSV파일은 sheet 개념 X

```python
DF2 = pd.read_excel('파일이름.xlsx')
DF2
```

* DataFrame 예시

![](https://github.com/soowoong0329/TIL/blob/master/img/dataframe(pandas).PNG?raw=true)

![](https://github.com/soowoong0329/TIL/blob/master/img/dataframe(DF1).PNG?raw=true)

#### Information

```python
type(DF1)

### pandas.core.frame.DataFrame
```

```python
DF1.Index

### RangeIndex(start=0, stop = 17 , step = 1)
```

```python
DF1.columns

### Index(['Name','Gender','Age','Grade','Picture','BloodType','Height','Weight',dtype='object'])
```

```python
DF1.values

### array([['송태섭','남자',21,3,'무','B',179.1,63.9],
###          [...]])형태로 value값만 출력 
```

```python
DF1.info()
```

![](https://github.com/soowoong0329/TIL/blob/master/img/DF1.info.PNG?raw=true)

```python
DF1.head()
```

![](https://github.com/soowoong0329/TIL/blob/master/img/df.head.PNG?raw=true)

```python
DF1[0:5]
```

![](https://github.com/soowoong0329/TIL/blob/master/img/df05.PNG?raw=true)

```python
DF1.tail(3)
```

![](https://github.com/soowoong0329/TIL/blob/master/img/dftail.PNG?raw=true)

```python
DF1[-3:]
```

![](https://github.com/soowoong0329/TIL/blob/master/img/df-3.PNG?raw=true)

```python
#요약통계자료(dType = 수치형만)
DF1.describe()
```

![](https://github.com/soowoong0329/TIL/blob/master/img/dfdescribe.PNG?raw=true)

---

## 시각화(Visualization)

* 2차원 공간에 시각화
* 연속형/명목형 datatype
* series단위로 생성

### In pandas

#### 1) 선 그래프

```python
import pandas as pd
DF1 = pd.read_csv('PII.csv')

DF1[['Height']].plot(kind = 'line', grid = True) # grid = True 뒷 배경 바둑판
```

#### 2) 막대 그래프

```python
DF1[['Height','Weight']].plot(kind = 'bar')
```

#### 3) 히스토그램

```python
DF1['Height'].plot(kind = 'hist', bins = 5, alpha = 0.5)
```

#### 4) 막대그래프

```python
DF1[['Height']].plot(kind = 'box')
```

#### 5) 산점도

```python
DF1[['Height','Weight']].plot(kind = 'scatter', x = 'Height', y = 'Weight', s = 50)
```

#### 6) 파이그래프

```python
DF1.BloodType.value_counts().plot(kind = 'pie')
```

---

### matplotlib

#### 1) 선 그래프

```python
import matplotlib.pyplot as plt
DF1 = pd.read_csv('PII.csv')
```

```python
plt.figure(figuresize = (9,6))
plt.plot(DF1.Height)
plt.grid(True)
plt.show()
```

#### 2) 막대 그래프

```python
plt.bar(DF1.index,DF1.Height, width = 0.3, color = 'g')
plt.show()
```

#### 3) 히스토그램

```python
plt.hist(DF1.Height, bin = 5, alpha= 0.5)
plt.show()
```

#### 4) 상자 그래프

```python
plt.boxplot(DF1.Height)
plt.show()
```

#### 5) 산점도

```python
plt.scatterr(DF1.Height, DF1.Weight, s = 50)
plt.show()
```

#### 6) 파이 그래프

```python
plt.pie(DF1.BloodType.value_counts(), label = DF1.BloodType.unique(), autopct = '%.1f%%')
plt.show()
```

---

### seaborn

#### 1) 회귀선 그리기

```python
import pandas as pd
import seaborn as sns
```

```python
sns.regplot(DF1.Height,DF1.Weight)
plt.show()
```

#### 2) 선 그래프

```python
sns.lineplot(DF1.index,DF1.Height)
plt.show()
```

#### 3) 막대 그래프 - 연속형

```python
sns.barplot(x = DF1.index, y = DF1.Height)
plt.show()
```

#### 4) 막대 그래프 - 명목형

```python
sns.countplot(DF1.BloodType)
plt.show()
```

#### 5) 히스토그램

```python
sns.distplot(DF1.Height)
plt.show()
```

#### 6) 상자그래프

```python
sns.boxplot(y = DF1.Height, x = DF1.Grade)
plt.show()
```

#### 7) 산점도

```python
sns.scatterplot(DF1.Height, DF1.Weight, s = 50)
plt.show()
```

---



