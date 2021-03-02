# Data Preprocessing

### apply()

* Dataframe을 특정조건에 맞는 값을 변경하기 위한 함수이다.

* titanic dataset 이용함.

```python
import seaborn as sns
titanic = sns.load_dataset('titanic')

DF = titanic.loc[:, ['age','fare']].head(5) # loc == 조회하기

DF
```

![](https://github.com/soowoong0329/TIL/blob/master/img/missing_data/axis.PNG?raw=true)


#### apply(axis = 0)

* `sum()`함수를 행(Row) 방향으로 매핑

  * column wise

  ```python
  DF.apply(sum, axis = 0)
  ```



#### apply(axis = 1)

* `sum()`함수를 열(Column) 방향으로 매핑

  * row wise

  ```python
  DF.apply(sum, axis = 1)
  ```

---

### Filtering

```python
import seaborn as sns
titanic = sns.load_dataset('titanic')

titanic.head(3)
```

* 'age' 가 10살 이상이면서 20살 미만

```python
Filter_1 = (titanic.age >= 10) & (titanic.age < 20)

titanic.loc[Filter_1, :].head()
```

* 'age'가 10살 미만이면서 'sex'이 여자

```python
Filter_2 = (titanic.age < 10) & (titanic.sex == 'female')

titanic.loc[Filter_2, :].head
```

* 'age'가 10살 미만 또는 60살 이상

```python
Filter_3 = (titanic < 10) | (titanic >= 60)

titanic.loc[Filter_3, ['age','sex','alone']].head()
```



#### `isin()`

* 'sibsp' 에 3 또는 4 또는  5를 포함

```python
Filter_isin = titanic['sibsp'].isin([3,4,5]) # sibsp ==3 | sibsp == 4 | sibsp == 5 와 같은 의미

titanic[Filter_isin].head(6)
```

---

### 데이터프레임 합치기

* DF1, DF2 생성

```python
import pandas as pd

DF1 = pd.DataFrame({'HP' : ['hp0','hp1','hp2','hp3'],
                    'IBM' : ['ibm0','ibm1','ibm2','ibm3'],
                    'DELL' : ['dell0','dell1','dell2','dell3']},
                    index = [0,1,2,3])

DF1
```

```python
DF2 = pd.DataFrame({'HP' : ['hp2','hp3','hp4','hp5'],
                    'IBM' : ['ibm2','ibm3','ibm4','ibm5'],
                    'DELL' : ['dell2','dell3','dell4','dell5'],
                    'ASUS' : ['asus2','asus3','asus4','asus5']},
                    index = [2,3,4,5])
DF2
```



#### `concat()`

* concatenate , 단순히 데이터를 연결한다.

```python
pd.concat([DF1,DF2],axis = 0)
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/concat.PNG?raw=true)

* ignore_index = True : 인덱스 연결한다.

```python
pd.concat([DF1,DF2],axis = 0, ignore_index = True)
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/concat_ignore.PNG?raw=true)

* 열기준 , axis = 1, inner join

```python
pd.concat([DF1,DF2], axis = 1, join ='inner')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/concatinner.PNG?raw=true)

* 열기준, axis =1, outer join

```python
pd.concat([DF1,DF2], axis = 1, join = 'outer')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/concatouter.PNG?raw=true)

---



### `merge()`

* 두 데이터프레임을 각 데이터에 존재하는 key값을 기준으로 병합할 때 사용한다.

```python
pd.merge(DF1,DF2)
```

* how = 'outer'

```python
pd.merge(DF1,DF2, how = 'outer')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/mergeouter.PNG?raw=true)

* how = 'left'

```python
pd.merge(DF1,DF2, how = 'left')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/mergeleft.PNG?raw=true)

* how = 'right'

```python
pd.merge(DF1,DF2, how = 'right')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/mergeright.PNG?raw=true)

---



## 그룹연산

```python
import seaborn as sns
titanic = sns.load_dataset('titanic')

DF = titanic.loc[:,['age','sex','class','fare','survived']]

DF.head()
```

* class 기준의 dataframe 생성

```python
grouped = DF.groupby['class']

grouped
```

* 결과 확인

  * first, second, third 키별 3줄씩 출력

  ```python
  for key in ['First', 'Second', 'Third'] :
      print(grouped.get_group(key).head(3))
      print('\n')
  ```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/grouped.PNG?raw=true)

```python
grouped.mean() # 그룹별 평균

grouped.get_group('Third').head(3) # 'Third' 키 그룹 정보 확인 : 특정 키 정보확인하기
```



* 두 개 key값 이용하여 groupby

```python
grouped_TWO = DF.groupby(['class','sex'])

grouped_TWO
```

* 결과 확인

```python
for key, group in grouped_TWO :
    print('* key :',key)
    print('* number :', len(group))
    print(group.head(3))
    print('\n')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/grouped2.PNG?raw=true)

```python
grouped_TWO.mean() # 그룹별 평균

grouped_TWO.get_group('First','female').head(3) # 그룹별 정보 확인
```

---



### `agg()`

* Aggregation : 여러 개의 함수를 groupby에 적용
  * 그룹별로 연산 결과를 집계하여 반환

```python
grouped.agg(['mean','std'])
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/agg.PNG?raw=true)

```python
grouped.agg({'fare' : ['mix','max'], 'age' : ['mean','std']})
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/agg2.PNG?raw=true)

---

### `transform()`

* 그룹별로 함수를 적용해 각 원소의 행과 열을 기준으로 연산 결과를 반환
  * z-score column 추가하기

```python
def z_score(x) :
    return (x - x.mean())/ x.std()
```

```python
DF['z_score'] = grouped.age.transform(z_score)

DF.head(3)
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/zscore.PNG?raw=true)

#### lambda

* 사용자 정의 함수를 문법에 맞추어 작성하는 것보다 쉽게 작성하게 해주는 함수

* `describe()` : 카운트,평균,표준편차,최대/최소값, 4분위수 테이블로 출력

```python
grouped.apply(lambda x: x.describe())
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/describe.PNG?raw=true)

---

## 멀티 인덱스

* pandas의 dataframe 의 인덱싱 함수 `loc`,`iloc`사용하려면 큰 그룹부터 인덱시 해야한다.
  * `.xs`사용하면 수준(level) 만 명시하면 인덱싱 가능하다.

```python
grouped_MI = DF.groupby(['class','sex'])

grouped_MI.mean()
```

```python
grouped_MI.mean().xs('First',level='class')
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/xsclass.PNG?raw=true)

```python
grouped_MI.mean().xs(['First','male'], level = ['class','sex'])
```

![](https://github.com/soowoong0329/TIL/blob/master/img/pandas_propreprocessing/xs2.PNG?raw=true)

---

### pivot_table()

* 구성요소
  * index : 행 인덱스
  * column  : 열 인덱스
  * values : 데이터
  * aggfunc : 적용함수

```python
import seaborn as sns
titanic = sns.load_dataset('titanic')

DF = titanic.loc[:, ['age','sex','class','fare','survived']]

DF.head(3)
```

```python
DF_1 = pd.pivot_table(DF,
                      index = 'class',
                      columns = 'sex',
                      values = 'age',
                      aggfunc = 'mean')

DF_1
```

* 2개 적용 함수

```python
DF_2 = pd.pivot_table(DF,
                      index = 'class',
                      columns = 'sex',
                      values = 'survived',
                      aggfunc = ['mean','sum'])

DF_2
```

* 다중인덱스, 다중데이터, 다중 함수

```python
DF_3 = pd.pivot_table(DF,
                      index = ['class','sex'],
                      columns = 'survived',
                      values = ['age','fare'],
                      aggfunc = ['mean','max'])

DF_3
```

#### 멀티 인덱스

```python
DF_3.index
DF_3.columns
```

> google for multi index

---

