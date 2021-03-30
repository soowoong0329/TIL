# Natural Language Processing : NLP

> 학습된 모델로 번역,문장 요약, 문자생성 등의 작업 수행

* 대량의 말뭉치(Corpus)를 모델 학습에 활용
  * 말뭉치 : 자연어 연구를 위해 특정 목적을 가지고 수집한 언어의 표본
* 자연어 처리의 **목적은 이해(Understanding)가 아님**
  * **연산(Computation)  or 처리(Processing) 영역**

* 수학적 연산을 위해 **언어를 숫자로 변환**하는 작업이 필요
* 인간이 사용하는 **자연어**를 컴퓨터가 연산할 수 있는 **벡터(Vector)**로 변환
  * Vector : 숫자의 나열

---

### Preprocessing

> 자연어 학습에 적합하도록 수집된 텍스트를 전처리 작업이 필요(Cleansing)

#### Tokenization

> 언어를 일정 단위로 잘라내는 것

* 수집된 말뭉치(Corpus)를 토큰(Token) 단위로 나누는 작업
  * 토큰의 단위는 **일반적으로 의미를 가지는 단위**로 정의
* 일반적으로 형태소(Morpheme) 단위로 토큰화 수행
  * **형태소란? : 의미를 가지는 가장 작은 말의 단위**

* Sentence , word, Character 단위 Tokenization
  * 문장, 단어, 영어의 경우 Character단위로 잘라내는 것
  * **Word Tokenization**(단어 토큰화)
  * **Sentence Tokenization**(문장 토큰화)
* **한국어의 경우 조사와 띄어쓰기 등으로 영어보다 토큰화가 어려움**
* Stop Words : 불용어 처리
  * 조사, 반복적 단어, 관사 등등을 제거하는 것
* Stemming, Lemmatization
  * 시제, ~ing, 복수형 등등을 원형 단어로 바꿔주는 것

#### Encoding

> 문자 --> 숫자 변환, Encoding 참고

* 정수 인코딩(Integer Encoding)
  * 단어를 고유한 정수에 맵핑
  * 단어가 2000개라면 각각 단어에 고유한 정수를 인덱스로 부여
* 원-핫 인코딩(One - Hot Encoding)
  * 단어 집합 크기의 벡터의 차원으로 0과 1을 사용하여 표현

---

### Language Model

* 언어(단어,문장)에 존재하는 현상을 표현하기 위해 **확률**을 할당하는 것
* 문장이 적절한지? , 말이 되는지 판단하기 위한 기준
  * P(승객이 버스에 탔다) vs P(승객이 버스에 태운다)
  * 나는 딥러닝을 ~ P(배운다) vs P(어렵다) vs P(고친다) vs P(가르친다)
* BoW(Bag of Words)
* n-gram
* TF-IDF(Term Frequency - Inverse Document Frequency)

#### Bag of Words

* 문서가 가지는 모든 단어(Words)를 **문맥이나 순서를 무시**하고 일괄적으로

  **문장에 포함된 단어에 대해 빈도 값을 부여**해 특징을 추출

* **발생빈도가 높을수록 중요한 단어**로 인식

* 장점
  * 쉽고 빠른 구축
  * 예상보다 문서의 특징을 잘 반영
* 단점
  * 언어의 특성상 자주 등장하는 단어에 높은 중요도를 부여
  * 단어의 순서를 고려하지 않아, 문맥 의미(Semantic Context) 반영 부족
  * 희소 행렬(Sparse Metrix)을 생성하여 학습 시간 증가 및 성능에 부정적 영향

* Bow - Feature Vectorization
  * M개의 문서(Document) 또는 문장(Sentence)
  * 모든 단어(Term) 추출 시 N종류의 단어 존재
  * M x N 크기의 행렬 생성
  * example

|      |  I   | like | dog  | You  | hate | bug  |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|  A   |  1   |  1   |  1   |  0   |  0   |  0   |
|  B   |  0   |  1   |  1   |  1   |  0   |  0   |
|  C   |  1   |  0   |  0   |  0   |  1   |  1   |

> A : I like dog
>
> B : You like dog
>
> C : I hate bug



#### n-gram

* BoW의 **단어 순서를 무시하는 단점 보완**

  * 1-gram(Unigram) , 2-gram(Bigram), 3-gram(Trigram)
  * Example
  * Machine Learning is fun and is not boring

  | Machine | Learning |  is  | fun  | and  | not  | boring |
  | :-----: | :------: | :--: | :--: | :--: | :--: | :----: |
  |    1    |    1     |  2   |  1   |  1   |  1   |   1    |

  | Machine | Learning |  is  | fun  | and  | not  | boring | Machine Learning | Not boring |
  | :-----: | :------: | :--: | :--: | :--: | :--: | :----: | :--------------: | :--------: |
  |    1    |    1     |  2   |  1   |  1   |  1   |   1    |        1         |     1      |

  

#### TF-IDF

> Term(==word) Frequency - Inverse Document Frequency

* BoW의 **단어의 빈도수만 고려하는 단점**보완
  * **개별 문서에 자주 나타나는 단어에 높은 가중치 부여**
  * 모든 문서에 전반적으로 자주 나타나는 단어에는 **패널티** 부여

* TF Score
  
  * **특정문서(Document)에 등장한 특정 단어(Term)의 등장 횟수**
* IDF Score
  
* **특정 단어(Term)가 등장한 문서(Document)의 수**
  
* Example

  * A : a new book, a used book , a book store
  * B : a dog in a dog house is big
  * TF Score : A

  |  a   | New  | book | used | store |
  | :--: | :--: | :--: | :--: | :---: |
  | 3/9  | 1/9  | 3/9  | 1/9  |  1/9  |

  * TF Score : B

  |  a   | dog  |  in  | house |  is  | big  |
  | :--: | :--: | :--: | :---: | :--: | :--: |
  | 2/8  | 2/8  | 1/8  |  1/8  | 1/8  | 1/8  |



* IDF Score

  * $$
    log ({{전체 문서의 수} \over 해당 \ 단어를 \ 포함하는 \  문서의 \ 수})
    $$

|      a       |      new       |      book      |      dog       |      big       |
| :----------: | :------------: | :------------: | :------------: | :------------: |
| log(2/2) = 0 | log(2/1) = 0.3 | log(2/1) = 0.3 | log(2/1) = 0.3 | log(2/1) = 0.3 |

* TF-IDF Score
  * TF - IDF(T) = TF(T) * log(M/IDF(T))

|      | a           | new             | book            | dog              | big             |
| ---- | ----------- | --------------- | --------------- | ---------------- | --------------- |
| A    | 3/9 * 0 = 0 | 1/9 * 0.3 = 0.3 | 3/9 * 0.3 = 0.1 | 0                | 0               |
| B    | 2/8 * 0 = 0 | 0               | 0               | 2/8 * 0.3 = 0.08 | 1/8 * 0.3 =0.03 |



---

### Similarity

* 단어나 문장 간 **유사도**를 비교
  * 단어나 문장을 **벡터로 변환 후 유사도를 비교**

#### Euclidean Distance similarity

* 벡터 간의 거리를 계산하여 유사도를 측정

* **거리가 짧을수록 유사도 높음**

* Example

  * $$
    ed1 = \sqrt {(5 - 5)^2 + (1 - 2)^2}
    $$

  * ed1 :  남자와 왕자의 유사도

  * ed2 :  남자와 공주의 유사도

  ![](C:\Users\samsung\Desktop\euclidean.PNG)

#### Cosine Similarity

* 벡터 간의 사잇각을 계산하여 유사도를 측정

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR2hNdNXc27gNEcmaTvYqxG0Rl1GTmJCIYeXA&usqp=CAU)

> *source : https://halalhassan.wordpress.com/2013/08/31/cosine-similarity-in-mapreduce-hadoop/*

* 사잇각이 작을 수록 유사도 높음
* 벡터의 크기가 아닌 방향성 기반

![](C:\Users\samsung\Desktop\cosine.PNG)

---

> Google Drive : NLP_Preprocessing, Cosine_Similarity



