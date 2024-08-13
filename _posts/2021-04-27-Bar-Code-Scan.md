---
navigation: true
title: Bar Code Scan Arduino
date: 2021-04-27
class: post-template
---

*this was a long time ago so the date isn't exact and I built this for a custom bar code.

This project is about a bar code scanner. The bar code is a thin piece of paper with white and black lines. The arduino has a photoresistor, where 
it senses if it is on a black or white square. And if the squares come through in a correct order, then a messege is displayed on an LCD screen. 

If the resistor is hooked up on a 10K resistor, it will read around 30-70 if it sees white. If black: it will read around 100-150.

Here is the simple code for the pattern I made:


```
#include <LiquidCrystal.h>
LiquidCrystal lcd(7, 8, 9, 10, 11, 12);

const int analogread = A0;
int sensor = 0;
int x;
int y;
int z;
int a;
int b;
int c;


void setup() {
  // put your setup code here, to run once:
Serial.begin(9600);
lcd.begin(16, 2);
}

void loop() {
  // put your main code here, to run repeatedly:
sensor = analogRead(A0);
Serial.println(sensor);
lcd.setCursor(0, 1);
delay(50);

if (sensor <= 80) {
  x = 2;
}
delay(25);
if (x == 2 && sensor < 140 && sensor > 90) {
  y = 3;
}
delay(25);
if ( y == 3 && sensor <= 80) {
z = 4;  
}
delay(25);
if ( z == 4 && sensor < 130 && sensor > 90) {
  a = 5;
}
delay(25);
if ( a == 5 && sensor <= 80) {
  b = 6;
}
delay(25);
if (b == 6 && sensor < 130 && sensor > 90) {
  c = 7;
}
delay(25);
if ( c == 7 && sensor <= 80) {
  lcd.println("Cheerios");
  lcd.print("Cereal");
}
delay(25);

}
```
