```C
#include <SoftwareSerial.h>
  #define RXD 8
  #define TXD 9

  SoftwareSerial blueToothSerial(TXD, RXD);

  int led_r = 13;
  int led_g = 12;
  int led_b = 11;

  int enA = 2;
  int in1 = 3;
  int in2 = 4;

  int i = 0; // 정지 시간 조절할 정수형 변수 i
  
  int state; // 앱 출발지 선택 처리 상황
  int floorloc; // 앱 도착지 선태 처리 상황
  
  int startfloor; // 시작 층
  int endfloor; // 도착 층
  int call = 0; // 명령 순서, 0: 시작 층 정하기, 1: 도착 층 정하기, 2: 모터 작동

  int now_floor; // 엘리베이터가 위치한 현재 층 수

void setup() {
  Serial.begin(9600);
  blueToothSerial.begin(9600);
  pinMode(led_r, OUTPUT);
  pinMode(led_g, OUTPUT);
  pinMode(led_b, OUTPUT);

  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  
  now_floor = 1;
}

void move_up(int moveS, int start, int endS)
{
  if (moveS <= 0)
    Serial.println("잘못된 move값 입니다.");
  
  while(start && endS) // 종료 조건은 층 값이 0
  {
    digitalWrite(in1, HIGH);
    digitalWrite(in2, LOW);  
    digitalWrite(enA, 10);
    delay(960 * moveS);//(이동층수 * 1초) 딜레이
          
    Serial.print(moveS);
    Serial.println("초 경과");
    if(i >= moveS)// 이동 층수만큼 시간이 지나면
    {
      // 정지 명령
      digitalWrite(in1, LOW);
      digitalWrite(in2, LOW);

      digitalWrite(enA,0);
      start = endS = 0; // 상황 종료
      break; 
    }
  }
}

void move_down(int moveS, int start, int endS)
{
  if (moveS <= 0)
    Serial.println("잘못된 move값 입니다.");
  
  while(start && endS) // 종료 조건은 층 값이 0
  {
    digitalWrite(in1, LOW);
    digitalWrite(in2, HIGH);  
    digitalWrite(enA, 10);
    delay(960 * moveS);//(이동층수 * 1초) 딜레이
          
    Serial.print(moveS);
    Serial.println("초 경과");
    if(i >= moveS)// 이동 층수만큼 시간이 지나면
    {
      // 정지 명령
      digitalWrite(in1, LOW);
      digitalWrite(in2, LOW);

      digitalWrite(enA,0);
      start = endS = 0; // 상황 종료
      break; 
    }
  }
}

void loop() {
  // 엘리베이터 얼굴 인식 호출
  if(blueToothSerial.available() > 0 && call == 0){
    state = blueToothSerial.read();
    Serial.print(char(state));
    Serial.println("층에서 호출");
    
    }

    // 1층에서 호출
    if(state == '1' && call == 0)
    {
      if (now_floor > 1)
        move_down(now_floor - 1, now_floor, 1);
      state = 0;
      call = 1;

      startfloor = 1;
      delay(1000);
    }

    // 2층에서 호출
    else if(state == '2' && call == 0)
    {
      if (now_floor > 2)
        move_down(now_floor - state, now_floor, 2);
      else if (now_floor < 2)
        move_up(2 - now_floor, now_floor, 2);
      
      state = 0;
      call = 1;

      startfloor = 2;
      delay(1000);
    }

    // 3층에서 호출
    else if(state == '3' && call == 0)
    {
      if (now_floor < 3)
        move_up(3 - now_floor, now_floor, 3);
      state = 0;
      call = 1;

      startfloor = 3;
      delay(1000);
    }

   

    // 엘리베이터 도착지 지정
    if(blueToothSerial.available() > 0 && call == 1)
    {
        floorloc = blueToothSerial.read();
        Serial.print(char(floorloc));
        Serial.println("도착지");
        delay(1000);
    }

    // 도착지가 1층일때
     if(floorloc == '4' && call == 1 )
    {
      
      floorloc = 0;
      call = 2;

      endfloor = 1;
      delay(1000);
    }

    // 도착지가 2층일때
    else if(floorloc == '5' && call == 1)
    {
      
      floorloc = 0;
      call = 2;

      endfloor = 2;
      delay(1000);
    }
    
    // 도착지가 3층일때
    else if(floorloc == '6' && call == 1)
    {
      
      floorloc = 0;
      call = 2;

      endfloor = 3;
      delay(1000);
    }


  	else 
    {
      // 모터 동작
      
      if (endfloor - startfloor > 0) // 시작층 < 도착층 -> 엘리베이터 UP
      {
        now_floor = endfloor;
        move_up(endfloor - startfloor, startfloor, endfloor);
      }
      else if (endfloor - startfloor < 0)//시작층 > 도착층 -> 엘리베이터 DOWN
      {
        now_floor = endfloor;
        move_down(startfloor - endfloor, startfloor, endfloor);
      }
    }
}
```
