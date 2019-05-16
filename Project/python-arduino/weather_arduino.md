### 날씨(맑음,흐림,비,기타 등)과 온도에 따라 LED 색이 변한다.
```script
#define OFFMODE -1
#define ONMODE 0
#define BLINKMODE 1
#define CLEAR 100
#define CLOUDS 101
#define RAIN 102
#define SNOW 103
#define THUNDERSTORM 104
#define MIST 105
const int RGB_RED=5;
const int RGB_GREEN=6;
const int RGB_BLUE=7;

const int pinLED_RED = 8;
const int pinLED_BLUE = 9;
const int pinLED_YELLOW = 10;
const int pinLED_GREEN = 11;
const int pinLED_ORANGE = 12;
const int pinLED_TEMPHIGH = 13;


char ch1;
char ch2;
int state = OFFMODE;

void setup() {
  pinMode(pinLED_RED,OUTPUT);
  pinMode(pinLED_YELLOW,OUTPUT);
  pinMode(pinLED_GREEN,OUTPUT);
  pinMode(pinLED_BLUE,OUTPUT);
  pinMode(pinLED_ORANGE,OUTPUT);
  pinMode(pinLED_TEMPHIGH,OUTPUT);
  pinMode(RGB_RED,OUTPUT);
  pinMode(RGB_GREEN,OUTPUT);
  pinMode(RGB_BLUE,OUTPUT);
  Serial.begin(9600);
}

void loop() {
  if(Serial.available()){
    ch1 = Serial.read();
    ch2 = Serial.read();
  }
  if(ch1=='r'){
    state=CLEAR;
  }else if(ch1=='g'){
    state=MIST;
  }
  else if(ch1=='b'){
    state=RAIN;
  }
  else if(ch1=='y'){
    state=CLOUDS;
  }
  else{
    state=THUNDERSTORM;
  }
if(ch2=='a'){
    analogWrite(RGB_RED,167);
    analogWrite(RGB_GREEN,0);
    analogWrite(RGB_BLUE,0);
  }else if(ch2=='b'){
    analogWrite(RGB_RED,200);
    analogWrite(RGB_GREEN,50);
    analogWrite(RGB_BLUE,0);
    }
    else if(ch2=='c'){
    analogWrite(RGB_RED,0);
    analogWrite(RGB_GREEN,160);
    analogWrite(RGB_BLUE,0);
    }
    else{
    analogWrite(RGB_RED,0);
    analogWrite(RGB_GREEN,0);
    analogWrite(RGB_BLUE,255);
    }

  if(state==CLEAR){
    digitalWrite(pinLED_RED,HIGH);
    delay(2000);
    digitalWrite(pinLED_RED,LOW);
  }else if(state==MIST){
    digitalWrite(pinLED_YELLOW,HIGH);
    delay(2000);
    digitalWrite(pinLED_YELLOW,LOW);
  }else if(state==RAIN){
    digitalWrite(pinLED_BLUE,HIGH);
    delay(2000);
    digitalWrite(pinLED_BLUE,LOW);
  }else if(state==CLOUDS){
    digitalWrite(pinLED_GREEN,HIGH);
    delay(2000);
    digitalWrite(pinLED_GREEN,LOW);
  }else {
    digitalWrite(pinLED_ORANGE,HIGH);
    delay(2000);
    digitalWrite(pinLED_ORANGE,LOW);
  }
}
```
