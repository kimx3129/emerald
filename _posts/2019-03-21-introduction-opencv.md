---
title: 이미지 프로세싱 & 컴퓨터 시각화 2부
---

안녕하세요. 지난시간에 우리는 이미지 프로세싱과 컴퓨터 시각화가 무엇인지 간략히 살펴보았으며 응용분야에 대해서도 짚어보았습니다. 2부 부터는 우리들도 기본기를 한번 다져보죠! 멋지지 않습니까? 꽤 긴 여정이 될 수도 있지만 그 긴 여정의 끝은 말로 다 형언할 수 없는 뿌듯함이 존재할꺼에요. 고진감래라는 옛말 기억하시죠? :)

여기서 저는 Python3를 사용할 것이며 Jupyter Notebook이라는 IDE를 가지고 코딩을 진행할 꺼에요. Jupyter Notebook이 뭔지 처음 들어보시는 분들도 계시겠지만 여기서 장황한 설명은 생략할께요^^ 검색하시면 아실꺼에요. 그리고 중요한 package 하나가 필요합니다. 바로 *opencv*라는 녀석입니다. 혹시라도 설치가 되어 있지 않다면 주저마시고 바로 설치를 해주세요. 그래야 저와 함께 여행을 하실 수 있으니깐요. Jupyter Notebook을 실행하고 새로운 workspace를 하나 생성할께요. 다음과 같군요. 아무것도 없습니다. 당연하죠~ 우리는 여기다 코딩을 시작할 꺼에요.

![empty_work](/emerald/img/empty_work.png "empty_work")  

[1] 페키지 불러오기 
다른 언어와 마찬가지로 파이썬도 수많은 페키지/라이브러리들을 제공합니다. 이것들을 import하여 우리의 작업공간에서 마음껏 사용할 수 있죠. 또한 무료이기 때문에 참 좋죠?
다음과 같은 페키지들을 기본적으로 불러옵니다 (아마 끝날때까지 제네들은 거의 계속 불러올 예정이에요)

```python
import numpy as np
import cv2
import matplotlib.pyplot as plt

%matplotlib inline
```

numpy는 파이썬에서 array형태의 데이터를 좀 더 효율적으로 많은 연산과 형태 변환 기능을 가능케 해주며 cv는 opencv페키지입니다. opencv2이기 때문에 페키지를 부를때 cv2입니다. 아....주 가끔 cv뒤에 왜 2를 붙이냐고 물어보는 사람이 있길래;;; matplotlib은 workspace에 이미지를 보여줄때 많이 쓰입니다. 물론 seaborn이라는 훌륭한 녀석도 존재하지만 저는 matplotlib을 쓸께요. 혹시나 모르는 분들이 계실까봐 노파심에서 부연설명을 아주 짧게 할께요. import할때 as라는 키워드를 쓰는데 페키지 이름이 너무 길경우 as(ALIAS)로 축약하여 사용할 수 있습니다. 맨 마지막 녀석 %matplotlib inline은 생소한 분들도 계시겠지만 저건 import하는것이 아닙니다. 이걸 넣어줘야 우리는 이미지를 작업공간에서 바로 볼 수 있습니다. 그렇지 않으면 우리는 

> <matplotlib.figure.Figure at 0x110b9c450>

이런 수수께끼스러운 문구를 우리들에게 보여주며 이미지는 보여주지 않는 삐뚤어지는 행동을 합니다. 따라서 이미지를 보기 위해선 %matplotlib inline를 실행시켜줘야 합니다~

자 그럼 돌립니다.  
 
![import](/emerald/img/import.png "Gray")

만약 아무런 에러가 없이 정상적으로 페키지들을 불러왔다면 우리는 아무런 에러메세지를 접하지 않을 꺼에요. 지금까지는 준비단계였어요. 이제부터 본격적으로 opencv에 대한 설명을 해야겠군요. pencv란 직접 웹사이트에 가서 긁어왔습니다. 영문이니 참고하세요. 자세한 정보는 직접 웹사이트에 방문하시면 되겠네요. (https://opencv.org/)
> OpenCV (Open Source Computer Vision Library) is released under a BSD license and hence it’s free for both academic and commercial use. It has C++, Python and Java interfaces and supports Windows, Linux, Mac OS, iOS and Android. OpenCV was designed for computational efficiency and with a strong focus on real-time applications. Written in optimized C/C++, the library can take advantage of multi-core processing. Enabled with OpenCL, it can take advantage of the hardware acceleration of the underlying heterogeneous compute platform.
  
그럼 저의 관점에서 설명해 볼께요. opencv는 파이썬을 포함함 몇가지 프로그래밍 언어를 사용하여 이미지 프로세싱과 컴퓨터 시각화를 다룰때 필수불가결한 페키지입니다. 마치 문을 열기 위해서 우리는 무조건 맞는 키를 사용해야만 문을 열 수 있듯이 우리는 원하는 목적을 이루기 위해서 opencv라는 페키지를 사용해야 합니다. 

![open_key](/emerald/img/open_key.png "Face_Rec")

아주 간단한 작업부터 한번 해보죠. 사진을 한번 불러와볼께요. 

```python
img = cv2.imread('DATA/minions.png')
```

끝이에요. cv2의 **imread** 라는 함수를 사용하여 이미지를 불러옵니다. 이미지가 어디에 위치해 있는지 구체적인 filepath를 명시해주면 됩니다. 저같은 경우에는 DATA폴더 안에 minions.png파일을 읽었군요. 그럼 이미지를 한번 불러와볼까요?

```python
plt.imshow(img)
```

![strange_minions](/emerald/img/strange_minions.png "strange_minions")

흠.. 색깔이 왜 저모양일까요?? 미니언즈는 원래 노란색인데... 흠.. 눈이 잘못된건지.. 이상하죠?? 흠.. 왜죠?? 컴퓨터가 고장났나요? 아니면 모니터가 갑자기 문제가 생겼나요?? 아닙니다!!! 컴퓨터는 RGB라는 색상의 체계가 있으며 opencv로 이미지를 불러올때 다른 형태로 불려와지기 때문입니다. 더 자세한 설명은 다음시간에 다룰께요. 더 설명이 길어지면 피곤할테니까요.

지금까지 우리는 opencv2에 대해 살짝 다뤄봤고 어떻게 사진을 불러오고 보여주는지에 대해 알아봤습니다. 다음 시간에는 어떻게 컴퓨터가 이미지를 인식하며 이미지 포멧을 좀 더 구체적으로 파헤쳐볼께요. 아직까지는 산넘어 산이지만 산을 다 넘다보면 언젠간 정상에 도달하겠죠? 거기다 깃발을 꽂아요!!

![what](/emerald/img/what.png "what")