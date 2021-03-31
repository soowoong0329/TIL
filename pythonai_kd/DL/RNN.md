# RNN : Recurrent Neural Network

> Recurrent : 순환/ 반복

* Feed - Forward Neural Network와의 차이점
  * **RNN은 전단계의 기억(short - term memory)을 가지고 동작**
    * 전 단계의 기억 == 이전 단계의 Output

<img src="https://www.researchgate.net/publication/338672883/figure/fig1/AS:864764884422656@1583187423806/The-comparison-between-Recurrent-Neural-Network-RNN-and-Feed-Forward-Neural-Network.jpg" style="zoom:67%;" />

> *source : https://www.researchgate.net/figure/The-comparison-between-Recurrent-Neural-Network-RNN-and-Feed-Forward-Neural-Network_fig1_338672883*

* RNN은 Hidden Layer가 하나만 있는 Deep Neural Network

  * DNN이면 Hidden Layer가 2개 이상들어가야 DNN

  * RNN은 Hidden Layer가 하나만 있음

    * Input --> Hidden Layer --> Output --> Hidden Layer --> Output2 --> Hidden Layer --> ...

    * **Hidden Layer가 하나만 있어도, 직전 단계에 처리한 Data의 Output이 다시 순환하여**

      **연속적으로 Data가 쌓여가면서 처리되기 때문에, Hidden Layer가 여러개 인것 처럼 동작**

---

#### DNN과 CNN 신경망

* 각 Layer간의 상태를 기억하지 않고, 입력과 출력이 독립적으로 처리
* **각 Layer마다 독립적**으로 가중치(Weight) 학습

#### 순환 신경망

* 내부 루프가 존재하는 신경망
* Hidden Layer의 출력이 계속 순환하면서 입력값과 함께 학습에 사용
* 연속적(Sequence) 데이터 처리를 위해서는 이전 단계의 정보가 필요
* 학습 단계에서 **모든 Layer가 같은 가중치를 공유**
  * 실제로 Hidden Layer는 1개 , 같은 parameter를 공유해서 사용

|  structure   |                                          |
| :----------: | :--------------------------------------: |
|  one to one  |               이미지 분류                |
| one to many  |             이미지 설명 문장             |
| many to one  | 여러 개 입력에 대한 감성 분석(긍정,부정) |
| many to many |      기계번역(영어문장 -> 한글문장)      |

![](http://karpathy.github.io/assets/rnn/diags.jpeg)

> *source : http://karpathy.github.io/2015/05/21/rnn-effectiveness/*



#### RNN

* 순차적인 정보를 처리하기 위한 모델
  * 앞 뒤 순서(상호관계) 가 존재하는 시계열 데이터
  * 텍스트나 음성 데이터 처리(번역,음성인식,음악,동영상)

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/rnncell.PNG?raw=true)

![](https://miro.medium.com/max/700/1*WMnFSJHzOloFlJHU6fVN-g.gif)

> *source :https://towardsdatascience.com/illustrated-guide-to-lstms-and-gru-s-a-step-by-step-explanation-44e9eb85bf21*
>
> *source : https://m.blog.naver.com/PostView.nhn?blogId=magnking&logNo=221311273459&proxyReferer=https:%2F%2Fwww.google.com%2F*



* RNN
  * Single Layer가 반복
  * Sequence Data 처리에 적합
  * 전 단계에 ht-1(전단계의 output) * Wh == 기억을 전달

![](https://github.com/soowoong0329/TIL/blob/master/img/DL/rnntanh.PNG?raw=true)

---

> Google Drive : ALL RNN files

