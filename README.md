# Face-Recognition-Elevator
## 아이디어 배경
- 집에서 호출하는 엘리베이터가 등장하는 트렌드에 맞춰 엘리베이터를 더욱 개선시킬 수 있는 방법에 대하여 논의
- 최근, 현정은 현대그룹 회장은 엘리베이터와 인공지능의 결합에 대해서 언급
- 노약자나 장애인이 많이 거주하는 지역에 AI엘리베이터를 설치하면 더욱 편리한 서비스를 제공할 수 있음

## 기능 설명
- 사전에 등록된 입주민의 얼굴을 인식하여 **호출된 층수** 에 엘리베이터가 자동으로 도달
- 각 층수에서 음성 또는 키패드를 통해 **도착할 층수** 를 입력하여 엘리베이터가 자동으로 도달                 
                   



## 엘리베이터 호출 단말
<img src="https://user-images.githubusercontent.com/81175672/185378527-8abceaf7-3d43-411b-884b-07e90e3f460d.gif"  width="300" height="500"/>                        

조작 단말은 스마트폰 앱을 만들어 엘리베이터 모듈 조작이 가능하도록 했습니다.                                          
스마트폰 앱은 **앱 인벤터** 를 사용하여 만들었으며 **얼굴인식** 에는 **PersonalImageClassifier API** , **음성인식** 에는 **google 음성인식** 을 사용했습니다.         
앱에서 내린 명령은 블루투스 통신을 통해 아두이노로 전송되고 아두이노는 수신된 명령어에 따라 작동합니다.
자세한 앱 제작은 [엘리베이터 호출 앱]() 을 참고해주세요.           

## 엘리베이터 모듈 제작
<img src="https://user-images.githubusercontent.com/81175672/185380484-313b5835-7334-4208-8c45-9fc025da8afc.jpg"  width="300" height="500"/>             

아두이노, 기어드 모터, 엘리베이터 키트, HC - 06를 사용하여 엘리베이터 모듈을 제작했습니다.          
자세한 아두이노 코드는 [엘리베이터 호출 모듈 코드](https://github.com/RyuJungSoo/Face_Recognition_Elevator/blob/main/%EC%95%84%EB%91%90%EC%9D%B4%EB%85%B8%20%EC%BD%94%EB%93%9C/%EC%95%84%EB%91%90%EC%9D%B4%EB%85%B8%20%EC%BD%94%EB%93%9C%20%EC%B5%9C%EC%A2%85.md) 를 참고해주세요.                 

## 시연영상
**< 얼굴인식 호출 및 음성인식 >**                       

https://user-images.githubusercontent.com/81175672/185382912-45973ccf-d05e-496c-81c5-a2dffa9bb513.mp4                    

***           
**< 키패드 >**              

https://user-images.githubusercontent.com/81175672/185383106-2ea7b2b4-da23-4863-880e-9260741a9276.mp4                

## 마무리하면서...

















