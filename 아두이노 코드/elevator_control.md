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
  int in3 = 5;
  int in4 = 6;
  int enB = 7;

  int i = 0; // 정지 시간 조절할 정수형 변수 i
  
  int state; // 앱 출발지 선택 처리 상황
  int floorloc; // 앱 도착지 선태 처리 상황
  
  int startfloor; // 시작 층
  int endfloor; // 도착 층
  int call = 0; // 명령 순서, 0: 시작 층 정하기, 1: 도착 층 정하기, 2: 모터 작동

void setup() {
  Serial.begin(9600);
  blueToothSerial.begin(9600);
  pinMode(led_r, OUTPUT);
  pinMode(led_g, OUTPUT);
  pinMode(led_b, OUTPUT);

  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);
  pinMode(enB, OUTPUT);
  pinMode(in3, OUTPUT);
  pinMode(in4, OUTPUT);
  

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
      digitalWrite(led_r, HIGH);
      delay(1000);
      digitalWrite(led_r, LOW);   
      state = 0;
      call = 1;

      startfloor = 1;
      delay(1000);
    }

    // 2층에서 호출
    else if(state == '2' && call == 0)
    {
      digitalWrite(led_g, HIGH);
      delay(1000);
      digitalWrite(led_g, LOW);
      state = 0;
      call = 1;

      startfloor = 2;
      delay(1000);
    }

    // 3층에서 호출
    else if(state == '3' && call == 0)
    {
      digitalWrite(led_b, HIGH);
      delay(1000);
      digitalWrite(led_b, LOW); 
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


    
    // 모터 동작
    i = 0; // i를 0으로 초기화
    
    // 출발지가 1층인 경우
    while(startfloor == 1 && endfloor == 2) // 도착지가 2층인 경우
    {
      digitalWrite(in1,LOW);
      digitalWrite(int2, HIGH);
      digitalWrite(int3, LOW);
      digitalWrite(int4, HIGH);
      digitalWrite(enA, 10);
      digitalWrite(enB, 10);
      delay(1000);

      i = i+1; // i값을 1씩 증가
      Serial.print(i);
      Serial.println("초 경과");
      while(i >= 1)
      {
        // 정지 명령
        digitalWrite(in1, LOW);
        digitalWrite(in2, LOW);
        digitalWrite(in3, LOW);
        digitalWrite(in4, LOW);
        digitalWrite(enA, 0);
        digitalWrite(enB, 0); 
        i++; //i를 1씩 증가
        if(i==2){ //i가 2와 같으면
        startfloor = endfloor = 0; // 상황 종료
        break; 
        }
      
      }

 
    while(startfloor == 1 && endfloor == 3) // 도착지가 3층인 경우
    {
      digitalWrite(in1,LOW);
      digitalWrite(int2, HIGH);
      digitalWrite(int3, LOW);
      digitalWrite(int4, HIGH);
      digitalWrite(enA, 10);
      digitalWrite(enB, 10);
      delay(1000);

      i = i+1; // i값을 1씩 증가
      Serial.print(i);
      Serial.println("초 경과");
      while(i >= 2)
      {
        // 정지 명령
        digitalWrite(in1, LOW);
        digitalWrite(in2, LOW);
        digitalWrite(in3, LOW);
        digitalWrite(in4, LOW);
        digitalWrite(enA, 0);
        digitalWrite(enB, 0); 
        i++; //i를 1씩 증가
        if(i==3){ //i가 3과 같으면
        startfloor = endfloor = 0; // 상황 종료
        break; 
        }
      
      }

      
    // 출발지가 2층인 경우
    while(startfloor == 2 && endfloor == 1) // 도착지가 1층인 경우
    {
      digitalWrite(in1,HIGH);
      digitalWrite(int2, LOW);
      digitalWrite(int3, HIGH);
      digitalWrite(int4, LOW);
      digitalWrite(enA, 10);
      digitalWrite(enB, 10);
      delay(1000);

      i = i+1; // i값을 1씩 증가
      Serial.print(i);
      Serial.println("초 경과");
      while(i >= 1)
      {
        // 정지 명령
        digitalWrite(in1, LOW);
        digitalWrite(in2, LOW);
        digitalWrite(in3, LOW);
        digitalWrite(in4, LOW);
        digitalWrite(enA, 0);
        digitalWrite(enB, 0); 
        i++; //i를 1씩 증가
        if(i==2){ //i가 2와 같으면
        startfloor = endfloor = 0; // 상황 종료
        break; 
        }
      
      }

 
    while(startfloor == 2 && endfloor == 3) // 도착지가 3층인 경우
    {
      digitalWrite(in1,LOW);
      digitalWrite(int2, HIGH);
      digitalWrite(int3, LOW);
      digitalWrite(int4, HIGH);
      digitalWrite(enA, 10);
      digitalWrite(enB, 10);
      delay(1000);

      i = i+1; // i값을 1씩 증가
      Serial.print(i);
      Serial.println("초 경과");
      while(i >= 1)
      {
        // 정지 명령
        digitalWrite(in1, LOW);
        digitalWrite(in2, LOW);
        digitalWrite(in3, LOW);
        digitalWrite(in4, LOW);
        digitalWrite(enA, 0);
        digitalWrite(enB, 0); 
        i++; //i를 1씩 증가
        if(i==2){ //i가 2와 같으면
        startfloor = endfloor = 0; // 상황 종료
        break; 
        }
      
      }


// 출발지가 3층인 경우
    while(startfloor == 3 && endfloor == 1) // 도착지가 1층인 경우
    {
      digitalWrite(in1,HIGH);
      digitalWrite(int2, LOW);
      digitalWrite(int3, HIGH);
      digitalWrite(int4, LOW);
      digitalWrite(enA, 10);
      digitalWrite(enB, 10);
      delay(1000);

      i = i+1; // i값을 1씩 증가
      Serial.print(i);
      Serial.println("초 경과");
      while(i >= 1)
      {
        // 정지 명령
        digitalWrite(in1, LOW);
        digitalWrite(in2, LOW);
        digitalWrite(in3, LOW);
        digitalWrite(in4, LOW);
        digitalWrite(enA, 0);
        digitalWrite(enB, 0); 
        i++; //i를 1씩 증가
        if(i==2){ //i가 2와 같으면
        startfloor = endfloor = 0; // 상황 종료
        break; 
        }
      
      }

 
    while(startfloor == 3 && endfloor == 2) // 도착지가 2층인 경우
    {
      digitalWrite(in1,HIGH);
      digitalWrite(int2, LOW);
      digitalWrite(int3, HIGH);
      digitalWrite(int4, LOW);
      digitalWrite(enA, 10);
      digitalWrite(enB, 10);
      delay(1000);

      i = i+1; // i값을 1씩 증가
      Serial.print(i);
      Serial.println("초 경과");
      while(i >= 2)
      {
        // 정지 명령
        digitalWrite(in1, LOW);
        digitalWrite(in2, LOW);
        digitalWrite(in3, LOW);
        digitalWrite(in4, LOW);
        digitalWrite(enA, 0);
        digitalWrite(enB, 0); 
        i++; //i를 1씩 증가
        if(i==3){ //i가 3과 같으면
        startfloor = endfloor = 0; // 상황 종료
        break; 
        }
      
      }



    
}
```
