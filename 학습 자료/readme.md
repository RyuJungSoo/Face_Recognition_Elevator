# 얼굴 인식 구현
엘리베이터를 호출하려면 **얼굴 인식**이 필요한데 해당 기능을 구현하는데 여러 방법이 있습니다.            
가장 쉬운 방법으로는 **앱인벤터 인공지능 API**를 사용하는 것이지만 핸드폰을 사용해야 하는 단점과 기능의 제약이 있습니다.                 
이러한 단점을 극복한 방법으로 **라즈베리파이와 카메라 모듈** 을 사용하여 얼굴 인식을 진행할 수 있습니다.
이 방법을 구현하는 과정은 많이 어렵지만 직접 시스템을 구현하고 임베비드에 조금 더 적합하다고 판단합니다.

# 1. 앱인벤터 인공지능 API
## [학습 과정 정리 블로그1](https://blog.naver.com/goldfox10/222825824708)                              
<img src="https://user-images.githubusercontent.com/81175672/181405923-d2b81445-618f-4300-8f89-06792ec8c055.png"  width="800" height="600"/>  

아래와 같이 블록코딩으로 구현할 수 있습니다.   

<img src="https://user-images.githubusercontent.com/94752167/181406915-d6564d86-2913-42ea-8c25-581413d6c2c7.png" width="800" height="600"/>  

<img src="https://user-images.githubusercontent.com/94752167/181406936-c55e3083-b023-44ad-bf7d-e1a98b0fe9f2.png" width="800" height="600"/>

<img src="https://user-images.githubusercontent.com/81175672/181135996-5dcd48cc-789c-4bff-b275-2429f2ba7653.jpg"  width="300" height="600"/>                     
앱인벤터는 여러 사물에 대해 학습되어 있는 학습 모델을 가져와서 사물 인식을 할 수 있는 API를 제공합니다.   
이에 따라, 사물을 인식하는 앱을 제작하여 여러 사물들을 인식시키는 실습을 진행하였습니다.
아쉬운 점이 있다면, 사물을 인식하는 툴을 사용하여 우리가 목표하고자 하는 얼굴인식은 하지 못했다는 점이 있습니다.


## [학습 과정 정리 블로그2](https://blog.naver.com/goldfox10/222825899977)               
<img src="https://user-images.githubusercontent.com/81175672/181136211-66810df9-33f1-4f3e-b72f-d7dbc52da5ec.jpg"  width="300" height="600"/>               
직접 모델을 학습한 후, 학습 모델을 불러와 사물 인식을 할 수 있는 API를 제공                     

[학습 모델 제작 사이트](https://classifier.appinventor.mit.edu/oldpic/)에서 모델 학습 후 앱인벤터에 업로드하여 적용
<img src="https://user-images.githubusercontent.com/81175672/181406091-30d0a59a-f842-4329-a0ef-c2d3ec49ede2.png"  width="800" height="600"/>    
<img src="https://user-images.githubusercontent.com/94752167/181407804-ac8b1c76-714b-44a1-a8f6-af890e696af2.png"  width="800" height="600"/>  
<img src="https://user-images.githubusercontent.com/94752167/181408401-7d3aa6cb-5c77-4a09-8ab9-64378299d370.png"  width="500" height="800"/>    

신라면과 진라면의 이미지를 학습시킨 모델을 가져와서 앱인벤터를 통해 신라면과 진라면을 분류하는 실습을 진행하였습니다.
만약 앱인벤터를 사용한다면 신라면과 진라면이 아닌 사람 얼굴을 학습시키는 방향을 실습할 예정입니다.

앞서 앱인벤터를 통해 실습한 것은 얼굴 인식 구현 방법 중 가장 쉬운 방법을 연습한 것 입니다.
앱인벤터가 쉽고 초보자도 따라할 수 있는 좋은 툴이 있어 많은사람들이 앱 만들기를 시작할 때 이용하면 좋을 것 같습니다.


# 2. 라즈베리파이 + 카메라 모듈
## 2.1 라즈베리파이 tensorflow 설치
[설치 과정 참고](https://m.blog.naver.com/PostView.naver?blogId=chandong83&logNo=221334936927&proxyReferer=https:%2F%2Fm.search.naver.com%2Fsearch.naver%3Fsm%3Dmtb_hty.top%26where%3Dm%26oquery%3D%25EB%259D%25BC%25EC%25A6%2588%25EB%25B2%25A0%25EB%25A6%25AC%25ED%258C%258C%25EC%259D%25B4%2B%25EB%25B8%2594%25EB%25A3%25A8%25ED%2588%25AC%25EC%258A%25A4%2B%25EB%258F%2599%25EA%25B8%2580%26tqi%3DhXudosqVWeKssOhzNb8ssssssnR-108914%26query%3D%25EB%259D%25BC%25EC%25A6%2588%25EB%25B2%25A0%25EB%25A6%25AC%25ED%258C%258C%25EC%259D%25B4%2B%25ED%2585%2590%25EC%2584%259C%2B%25ED%2594%258C%25EB%25A1%259C%2B)                                         

## 2.2 라즈베리파이 + teachable machine
[참고 자료1](https://ai-creator.tistory.com/26)                        
[참고 자료2](https://doljokilab.tistory.com/27)                             

## 2.3 라즈베리파이 + face recognition 라이브러리
[라이브러리 설치 및 실습](https://ukayzm.github.io/python-face-recognition/)                       
[참고 자료1](https://bskyvision.com/1089)                                  
[참고 자료2](https://www.teknotut.com/en/facial-recognition-with-raspberry-pi-and-opencv/)

***
# 3. 07.25~07.29 실습 결론
- 라즈베리파이 세팅시 파이썬과 라즈베리파이 버전이 안맞아 설치가 어려웠으며 라이브러리 호환 또한 되지 않았다.
- 특히, 중요한 Tensorflow가 호환되지 않았다. 블로그를 통해 많이 찾아봤고 초기화를 하고 다시 시도해봤지만 되지 않았다.
- 먼저 다음 실습 때, Tensorflow세팅을 다시 시도해보고, 만약 이것이 되지 않는다면 앱인벤터로 호출을 시도하는 것을 할 것이다.
- 또한, 다음 실습 때, 라즈베리파이 + teachable machin과 face recognition를 시도하여 어떤 것이 더 적합한지 알아볼 예정이다.
