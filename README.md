# miniproject-iot-code
#include <LiquidCrystal.h>
#include <stdio.h>
#include <Servo.h>
#define trigPin A0
#define echoPin A1
#define trigPin1 A2
#define echoPin1 A3

LiquidCrystal lcd(8, 9, 10, 11, 12, 13);

char inChar;
int IR=7;
Servo servo1;
int i=0;
unsigned int rain_sensor;




void setup() {
pinMode(IR, INPUT);
lcd.begin(16, 2);
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(trigPin1, OUTPUT);
pinMode(echoPin1, INPUT);
Serial.begin(115200);
lcd.clear();
lcd.clear();
lcd.setCursor(0,0);
lcd.print(" SMART DUMP");
lcd.setCursor(0,1);
lcd.print("MANAGEMENT SYSTEM");



delay(3000);
servo1.write(60); 
delay(2000);
erial.write("AT");
delay(1000);
Serial.write("ATE0");
delay(1000);
Serial.write("AT+CWMODE=3");
delay(1000);
Serial.write("AT+CIPMUX=1");
delay(1000);
Serial.write("AT+CIPSERVER=1,23");
delay(1000);
lcd.clear();
lcd.print("WITING FOR CONNECT");
delay(2000); 

}









void loop()
{
long duration, distance;
long duration1, distance1;
digitalWrite(trigPin, 0); 
delayMicroseconds(2);
digitalWrite(trigPin, 1);
delayMicroseconds(10); 
digitalWrite(trigPin, 0);
duration = pulseIn(echoPin, 1);
digitalWrite(trigPin1, 0); 
delayMicroseconds(2); 
digitalWrite(trigPin1, 1);





delayMicroseconds(10); 
digitalWrite(trigPin1, 0);
duration1 = pulseIn(echoPin1, 1);
delay(30); 

lcd.clear();
lcd.setCursor(0,0);
lcd.print("S1:");
lcd.print(distance);
lcd.print("CM");
lcd.setCursor(0,1);
lcd.print("S2:");
lcd.print(distance1);
lcd.print("CM");

if(digitalRead(IR)==0)
{

rain_sensor=analogRead(A5); 
lcd.clear();
lcd.setCursor(0,0);
lcd.print("WAITING FOR ");
lcd.setCursor(0,1);
lcd.print("GARBAGE");
rain_sensor=analogRead(A5); 
delay(1000);







if(rain_sensor<700)

{
lcd.clear();





lcd.setCursor(1, 0);
lcd.print("WET GARBAGE");
lcd.setCursor(1, 1);
lcd.print("*****");
servo1.write(120);
delay(5000);
servo1.write(60); 
delay(1000);
Serial.write("AT+CIPSEND=0,18");
delay(200);
Serial.write("WET GARBAGE");
Serial.write(" ");

}






if(!(rain_sensor<700))

{
lcd.clear();
lcd.setCursor(1, 0);
lcd.print("DRY GARBAGE");
lcd.setCursor(1, 1);
lcd.print("*****");
delay(3000);
servo1.write(5);
delay(5000);
servo1.write(60); 
delay(1000);
Serial.write("AT+CIPSEND=0,18");
delay(200);
Serial.write("DRY GARBAGE");
Serial.write(" ");
}
}  
![image](https://github.com/satwik8005/miniproject-demo/assets/143406522/1e8fe611-be24-403a-ab8b-af4d038aeeab)

