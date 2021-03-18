# Keras TensorFlow

* 데이터 흐름 프로그래밍을 위한 Open Software Library
* Neural Network 같은 Machine Learning 프로그램에 활용

### Tensor

* **다차원 행렬**
* Neural Network 학습의 기본 데이터 단위
  * 숫자(Numeric) 데이터를 담기 위한 컨테이너
  * float(실수)를 담기위한 컨테이너

* 차원(Dimension) , 축(Rank)을 가짐

| Rank |      Type       |                   Example                   |
| :--: | :-------------: | :-----------------------------------------: |
|  0   |     Scalar      |                      0                      |
|  1   |     Vector      |                    [0,1]                    |
|  2   |     Matrix      |                [[0,1],[1,0]]                |
|  3   | 3 Tensor(Array) | [[[0,0],[0,0]],[[1,1],[1,1]],[[2,2],[2,2]]] |
|  N   |    N Tensor     |                                             |



#### Tensor in NLP(Natural Language Processing)

* 문장과 단어를 숫자 벡터로 매핑
* EX

|  Word  | Index | One - Hot Encoding Vector |
| :----: | :---: | :-----------------------: |
|  하얀  |   0   |         [1,0,0,0]         |
| 고양이 |   1   |         [0,1,0,0]         |
| 강아지 |   2   |         [0,0,1,0]         |
| 비둘기 |   3   |         [0,0,0,1]         |

* 하얀 고양이 : [[1,0,0,0],[0,1,0,0]]
* 하얀 강아지 : [[1,0,0,0],[0,0,1,0]]
* 하얀 비둘기 : [[1,0,0,0],[0,0,0,1]]

* mini - batch Input(Rank3 ,3Dimention 형태)
  * 하얀 고양이  하얀 강아지  하얀 비둘기
  * [[[1,0,0,0],[0,1,0,0]],[[1,0,0,0],[0,0,1,0]],[[1,0,0,0],[0,0,0,1]]]

---

#### Tensor in Grayscale Image

* 흑백이미지 : 0 ~ 255
  * 흰색 : 255 , 검은색 : 0
* (3,5,5) : Rank 3 Tensor
* (Number of Images, Rows, Columns)

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/grayimg.PNG?raw=true)

#### Tensor in RGB Color Image

* (3,5,5,3) : Rank 4 Tensor
* (Number of Images, Rows, Columns, RGB Chnnel)

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/rgbimg.PNG?raw=true)

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/rgb3d.PNG?raw=true)

---

#### Tensor in RGB Color Video

* (3,5,600,800,3) : Rank 5 Tensor
* (Video Frames, Number of Images, Rows, Columns, RGB Channel)

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/video.PNG?raw=true)

---

### Keras Modeling

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/modelingkeras.PNG?raw=true)



---

> 실습 google. drive

