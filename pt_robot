#include <SoftwareSerial.h>

#include <DFRobotDFPlayerMini.h>

#include <Servo.h>

#include <Stepper.h>

#include <math.h>

#include <LedControl.h>

#include "dot.h"

 

char result;

char condition;

int squart_count = 0;

long squart_cal; //squart 칼로리 하나에 0.7

int handsup_count = 0;

long handsup_cal; //handsup 칼로리 0.5

int wrestle_count = 0;

long wrestle_cal; //wrestle 칼로리 0.6

int goal = 0;

int val;

unsigned long time; //운동후 지난 시간

boolean wakeup=false;

long randNumber; //랜덤 숫자

 

Servo myservo1; //왼팔

Servo myservo2; //오른팔

const int stepsPerRevolution = 2048;

Stepper myStepper(stepsPerRevolution, 11, 9, 10, 8);

SoftwareSerial MP3Module(2, 3);

DFRobotDFPlayerMini MP3Player;

unsigned long delaytime=100;

LedControl lc=LedControl(12, 11, 10, 1);//왼쪽

LedControl led=LedControl(6, 5, 3, 1);//오른쪽

 

void setup() {

  // put your setup code here, to run once:

  Serial.begin(9600);

  

  //mp3

  MP3Module.begin(9600);

   if (!MP3Player.begin(MP3Module)) { // MP3 모듈을 초기화합니다. 초기화에 실패하면 오류를 발생시킵니다.

    Serial.println(F("Unable to begin:"));

    Serial.println(F("1.Please recheck the connection!"));

    Serial.println(F("2.Please insert the SD card!"));

    //while (true);-주석시 잘 돌아감

  }

  delay(1);

  MP3Player.volume(30);  // 볼륨을 조절합니다. 0~30까지 설정이 가능합니다.

 

  //lcd

  //stepping 모터

  myStepper.setSpeed(10); //모터 속도 설정

  //servo 모터

  myservo1.attach(5);

  myservo2.attach(6);

  //가변저항으로 goal 설정

  //터치센서

  lc.shutdown(0,false);

  lc.setIntensity(0,8);

  lc.clearDisplay(0); //왼쪽 8*8dot

  led.shutdown(0,false);

  led.setIntensity(0,8);

  led.clearDisplay(0); //오른쪽 8*8dot

  MP3Player.play(1); 

}

 

void loop() {

  

  // put your main code here, to run repeatedly:

  if(squart_count>0 || handsup_count>0 || wrestle_count>0){ //운동 시작하면

    wakeup=true;

  }

  else { //운동 안하고있으면

    wakeup=false;

  }

  if(wakeup == false){ //운동 시작 안했을때 3일마다 깨우기

    time = millis(); //시간 재기

    if(time > 259200000){ //3일 지나면

      MP3Player.play(30); //깨우기

      time=0; //time 초기화

    }

  }

  randomSeed(analogRead(0)); //아날로그 0번 랜덤시드(랜덤값 계속 바뀌게 함)

  //test code

  MP3Player.play(1);  // 0001.mp3를 재생합니다.

  while (Serial.available() > 0) { 

    val = analogRead(A0);

    val = map(val, 0, 1023, 0, 100); //100개까지

    goal = val; //목표 설정

    result = Serial.read(); //Teachable machine 결과값

    switch (result) 

    {

      case '0': //stand 

        if (condition == '3') { //handsup -> stand : +1

          handsup_count++;

          Serial.println(handsup_count);

          //오디오

          MP3Player.play(handsup_count); //15개까지 음성은 저장됨

          delay (10);

          if (handsup_count % 5 == 0) { //10개씩마다

            myservo1.write(180);

            myservo2.write(180);//팔 들어올리기(모터)

            MP3Player.play(32); //잘하고있어요

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0);

          }

          if (handsup_count==1){

              for (int j=0; j<9;j++) 

                 {led.setRow(0, j, z_one[j]);

                  }//8*8 dot

             }else if (handsup_count==2){

                for (int j=0; j<9;j++) 

               {led.setRow(0, j, z_two[j]);

                }//8*8 dot

            }else if (handsup_count==3){

            for (int j=0; j<9;j++) 

               {led.setRow(0, j, z_three[j]);

               }//8*8 dot

            }else if (handsup_count==4){

                  for (int j=0; j<9;j++) 

                      {led.setRow(0, j, z_four[j]);

                       }//8*8 dot

           }else if (handsup_count==5){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_five[j]);

                  }//8*8 dot

           }else if (handsup_count==6){

                for (int j=0; j<9;j++) 

                   {led.setRow(0, j, z_six[j]);

                   }//8*8 dot

          }else if (handsup_count==7){

               for (int j=0; j<9;j++) 

                  {led.setRow(0, j, z_seven[j]);

                   }//8*8 dot

          }else if (handsup_count==8){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_eight[j]);

                }//8*8 dot

          }else if (handsup_count==9){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_nine[j]);

                }//8*8 dot

          }else if (handsup_count==10){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_zero[j]);

                }//8*8 dot

        }else if (handsup_count==11){

              for (int j=0; j<9;j++) 

                  {led.setRow(0, j, o_one[j]);

                  }//8*8 dot

        }else if (handsup_count==12){

             for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_two[j]);

                  }//8*8 dot

       }else if (handsup_count==13){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_three[j]);

                 }//8*8 dot

      }else if (handsup_count==14){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_four[j]);

                  }//8*8 dot

      }else if (handsup_count==15){

           for (int j=0; j<9;j++) 

              {led.setRow(0, j, z_five[j]);

                }//8*8 dot

      }else if (handsup_count==16){

           for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_six[j]);

                }//8*8 dot

      }else if (handsup_count==17){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_seven[j]);

                }//8*8 dot

      }else if (handsup_count==18){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_eight[j]);

                }//8*8 dot

      }else if (handsup_count==19){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_nine[j]);

                }//8*8 dot

      }else if (handsup_count==20){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, t_zero[j]);

                }//8*8 dot

  };//led

        }

        condition = '0';

        Serial.println("0");

        break;

      case '1': //squart

          for (int i=0; i<9;i++) 

             {lc.setRow(0, i, squart[i]);

             }//8*8 dot

          for (int j=0; j<9;j++) 

             {led.setRow(0, j, n_zero[j]);

             }//8*8 dot//led의 초기 상태    

      if (condition == '0') { //stand -> squart : +1

          squart_count++;

          Serial.println(squart_count);

          squart_cal = round(squart_count*0.7); //반올림하기 

          //오디오

          MP3Player.play(squart_count); //15까지

          delay (10);

          if (squart_count % 5 == 0 && squart_count % 10 != 0) { //5개씩마다-0

            //팔 들어올리기(모터)

            myservo1.write(180); //180

            myservo2.write(180); //180

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0);

            delay(1000);

            //mp3

            MP3Player.play(32); //잘하고있어요

            delay(10);

          }

          else if (squart_count % 5 == 0 && squart_count % 10 == 0) { //5개씩마다-1

            //팔 들어올리기(모터)

            myservo1.write(180); //180

            myservo2.write(0);

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0); //0

            delay(1000);

            //mp3

            MP3Player.play(33); //화이팅 힘내세요

            delay(10);

          }

          if (squart_count==1){

              for (int j=0; j<9;j++) 

                 {led.setRow(0, j, z_one[j]);

                  }//8*8 dot

             }else if (squart_count==2){

                for (int j=0; j<9;j++) 

               {led.setRow(0, j, z_two[j]);

                }//8*8 dot

            }else if (squart_count==3){

            for (int j=0; j<9;j++) 

               {led.setRow(0, j, z_three[j]);

               }//8*8 dot

            }else if (squart_count==4){

                  for (int j=0; j<9;j++) 

                      {led.setRow(0, j, z_four[j]);

                       }//8*8 dot

           }else if (squart_count==5){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_five[j]);

                  }//8*8 dot

           }else if (squart_count==6){

                for (int j=0; j<9;j++) 

                   {led.setRow(0, j, z_six[j]);

                   }//8*8 dot

          }else if (squart_count==7){

               for (int j=0; j<9;j++) 

                  {led.setRow(0, j, z_seven[j]);

                   }//8*8 dot

          }else if (squart_count==8){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_eight[j]);

                }//8*8 dot

          }else if (squart_count==9){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_nine[j]);

                }//8*8 dot

          }else if (squart_count==10){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_zero[j]);

                }//8*8 dot

        }else if (squart_count==11){

              for (int j=0; j<9;j++) 

                  {led.setRow(0, j, o_one[j]);

                  }//8*8 dot

        }else if (squart_count==12){

             for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_two[j]);

                  }//8*8 dot

       }else if (squart_count==13){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_three[j]);

                 }//8*8 dot

      }else if (squart_count==14){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_four[j]);

                  }//8*8 dot

      }else if (squart_count==15){

           for (int j=0; j<9;j++) 

              {led.setRow(0, j, z_five[j]);

                }//8*8 dot

      }else if (squart_count==16){

           for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_six[j]);

                }//8*8 dot

      }else if (squart_count==17){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_seven[j]);

                }//8*8 dot

      }else if (squart_count==18){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_eight[j]);

                }//8*8 dot

      }else if (squart_count==19){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_nine[j]);

                }//8*8 dot

      }else if (squart_count==20){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, t_zero[j]);

                }//8*8 dot//led

        }      

        condition = '1';

        Serial.println("1");

        break;

      case '2': //vent

        if (condition == '0' || condition == '1') { //stand -> vent 또는 squart -> vent : X

            MP3Player.play(31); //자세를 고쳐볼까요? 음성출력

            for (int i=0; i<9;i++) 

             {lc.setRow(0, i, l_ang_eye[i]);

             }//8*8 dot

          for (int j=0; j<9;j++) 

             {led.setRow(0, j, r_ang_eye[j]);

             }//led

         }

        condition = '2';

        Serial.println("1");

        break;

      case '3': //handsup

          for (int i=0; i<9;i++) 

             {lc.setRow(0, i, handsup[i]);

             }//8*8 dot

          for (int j=0; j<9;j++) 

             {led.setRow(0, j, n_zero[j]);

             }//8*8 dot//led의 초기 상태

      if (condition == '0') { //stand -> handsup : +1    

          handsup_count++;

          Serial.println(handsup_count);

          handsup_cal = round(handsup_count*0.7); //반올림하기

          //오디오

          MP3Player.play(handsup_count); //15까지

          delay (10);

          //5개마다 차례대로 음성 출력

          if (handsup_count % 5 == 0 && handsup_count % 10 != 0) { //5개씩마다-0

            //팔 들어올리기(모터)

            myservo1.write(180); //180

            myservo2.write(180); //180

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0);

            delay(1000);

            //mp3

            MP3Player.play(32); //잘하고있어요

            delay(10);

          }

          else if (handsup_count % 5 == 0 && handsup_count % 10 == 0) { //5개씩마다-1

            //팔 들어올리기(모터)

            myservo1.write(180); //180

            myservo2.write(0);

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0); //0

            delay(1000);

            //mp3

            MP3Player.play(33); //화이팅 힘내세요

            delay(10);

          }

        }       

        condition = '3';

        Serial.println("1");

        handsup_cal = round(handsup_count*0.7); //반올림하기

        break;

      case '4': //wrestle

      if (condition == '0') { //stand -> wrestle : +1

          wrestle_count++;

          Serial.println(wrestle_count);

          wrestle_cal = round(wrestle_count*0.7); //반올림하기

          //오디오

          MP3Player.play(wrestle_count); //15까지

          delay (10);

          //5개마다 차례대로 음성 출력

          if (wrestle_count % 5 == 0 && wrestle_count % 10 != 0) { //5개씩마다-0

            //팔 들어올리기(모터)

            myservo1.write(180); //180

            myservo2.write(180); //180

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0);

            delay(1000);

            //mp3

            MP3Player.play(32); //잘하고있어요

            delay(10);

          }

          else if (wrestle_count % 5 == 0 && wrestle_count % 10 == 0) { //5개씩마다-1

            //팔 들어올리기(모터)

            myservo1.write(180); //180

            myservo2.write(0);

            delay(1000);

            myservo1.write(0); //0

            myservo2.write(0); //0

            delay(1000);

            //mp3

            MP3Player.play(33); //화이팅 힘내세요

            delay(10);

          }

          if (wrestle_count==1){

              for (int j=0; j<9;j++) 

                 {led.setRow(0, j, z_one[j]);

                  }//8*8 dot

             }else if (wrestle_count==2){

                for (int j=0; j<9;j++) 

               {led.setRow(0, j, z_two[j]);

                }//8*8 dot

            }else if (wrestle_count==3){

            for (int j=0; j<9;j++) 

               {led.setRow(0, j, z_three[j]);

               }//8*8 dot

            }else if (wrestle_count==4){

                  for (int j=0; j<9;j++) 

                      {led.setRow(0, j, z_four[j]);

                       }//8*8 dot

           }else if (wrestle_count==5){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_five[j]);

                  }//8*8 dot

           }else if (wrestle_count==6){

                for (int j=0; j<9;j++) 

                   {led.setRow(0, j, z_six[j]);

                   }//8*8 dot

          }else if (wrestle_count==7){

               for (int j=0; j<9;j++) 

                  {led.setRow(0, j, z_seven[j]);

                   }//8*8 dot

          }else if (wrestle_count==8){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_eight[j]);

                }//8*8 dot

          }else if (wrestle_count==9){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, z_nine[j]);

                }//8*8 dot

          }else if (wrestle_count==10){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_zero[j]);

                }//8*8 dot

        }else if (wrestle_count==11){

              for (int j=0; j<9;j++) 

                  {led.setRow(0, j, o_one[j]);

                  }//8*8 dot

        }else if (wrestle_count==12){

             for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_two[j]);

                  }//8*8 dot

       }else if (wrestle_count==13){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_three[j]);

                 }//8*8 dot

      }else if (wrestle_count==14){

              for (int j=0; j<9;j++) 

                {led.setRow(0, j, o_four[j]);

                  }//8*8 dot

      }else if (wrestle_count==15){

           for (int j=0; j<9;j++) 

              {led.setRow(0, j, z_five[j]);

                }//8*8 dot

      }else if (wrestle_count==16){

           for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_six[j]);

                }//8*8 dot

      }else if (wrestle_count==17){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_seven[j]);

                }//8*8 dot

      }else if (wrestle_count==18){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_eight[j]);

                }//8*8 dot

      }else if (wrestle_count==19){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, o_nine[j]);

                }//8*8 dot

      }else if (wrestle_count==20){

          for (int j=0; j<9;j++) 

              {led.setRow(0, j, t_zero[j]);

                }//8*8 dot//led

        }       

        condition = '3';

        Serial.println("1");

        break;

    }

    if (squart_count == goal || handsup_count == goal || wrestle_count == goal) {

      //목표치 달성시 춤추기

      Serial.println("목표달성");

      //목표달성 mp3

      MP3Player.play(34);

      //팔 만세 - servo 모터

      myservo1.write(180); //180

      myservo2.write(180); //180

      delay(100);

      //몸통 30도씩 도리도리 돌기

      myStepper.step(170); //한 30도

      delay(1000);

      myStepper.step(-170); //한 30도

      delay(1000);

      myservo1.write(0); //0

      myservo2.write(0);

      delay(1000);

      uint8_t temp = random(0, 3); 

      if (temp ==0){ //33%의 확률로

        MP3Player.play(0); //한번 더 해봐요! 음성출력

      }

      //mp3

      MP3Player.play(34); //오늘 운동 수고했어 mp3

      delay(10);

      squart_count = 0; //초기화

      handsup_count = 0;

      wrestle_count=0;

    }

    else if (squart_count == goal - 2 || handsup_count == goal - 2 || wrestle_count == goal-2) {

      MP3Player.play(35); //마지막 두개만 더

      delay(1000);

      Serial.println("마지막 두개만 더");

    }

   

  }

  delay(100);

 

}
