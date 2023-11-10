# Arduino_beginner
Код и схемы

## SENSORS 
```C++
void setup() {
  Serial.begin(9600);
  Serial.println("Hello");
  pinMode(7, OUTPUT);
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
}

void loop() {
  int photores = analogRead(A0);
  int ptrn = analogRead(A1);

  if(photores > ptrn){
      digitalWrite(7, HIGH);
  }
  else {
    digitalWrite(7, LOW);
  }

  Serial.print("Photo: ");
  Serial.print(photores);
  Serial.print(", ");
  Serial.print("Ptr: ");
  Serial.println(ptrn);
}
```
## Светофор
```C++
void setup() {
  Serial.begin(9600);
  Serial.println("Hello");
  pinMode(7, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(4, OUTPUT);
}

void loop() {
  
  digitalWrite (7, HIGH);
  delay(500);
  digitalWrite (7, LOW);
  delay(200);
  digitalWrite (6, HIGH);
  delay(500);
  digitalWrite (6, LOW);
  delay(200);
  digitalWrite (4, HIGH);
  delay(500);
  digitalWrite (4, LOW);
  delay(200);
}
```
## BUTTON

```C++
#define BTN 9
#define LED1 7
#define LED2 6
#define LED3 4

void setup() {
  Serial.begin(9600);
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
  pinMode(BTN, INPUT);
}

void loop() {
  
  int btnVal = digitalRead(BTN);

  if(btnVal == 0){
    digitalWrite(LED1, HIGH);
    digitalWrite(LED2, HIGH);
    digitalWrite(LED3, HIGH);
  }
  else{
    digitalWrite(LED1, LOW);
    digitalWrite(LED2, LOW);
    digitalWrite(LED3, LOW);
  }

}
```
```C++
#define BTN 9
#define LED1 7
#define LED2 6
#define LED3 4

bool btnState = false;

void setup() {
  Serial.begin(9600);
  pinMode(LED1, OUTPUT);
  pinMode(LED2, OUTPUT);
  pinMode(LED3, OUTPUT);
  pinMode(BTN, INPUT);
}

void loop() {
  
  int btnVal = digitalRead(BTN);

  if(btnVal == 0){
    btnState = !btnState;
    // ! - логическое отрицание (смена переменной на противоположное значение)
  }

  if(btnState){
    // if(btnState) = if(btnState == true)
    digitalWrite(LED1, HIGH);
    digitalWrite(LED2, HIGH);
    digitalWrite(LED3, HIGH);
  }
  else{
    digitalWrite(LED1, LOW);
    digitalWrite(LED2, LOW);
    digitalWrite(LED3, LOW);
  }

}

```
## RGBLed
[GitHub](https://github.com/wilmouths/RGBLed)

```C++
#include <RGBLed.h>

#define RED_PIN 6
#define BLUE_PIN 5
#define GREEN_PIN 3

RGBLed led(RED_PIN, GREEN_PIN, BLUE_PIN, RGBLed::COMMON_ANODE);

void setup() {
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(RED_PIN, OUTPUT);
  pinMode(BLUE_PIN, OUTPUT);
}

void loop() {
  led.crossFade(255, 0, 0, 0, 255, 0, 5, 500); 
}
```
## Temperature
```C++
// библиотека для работы с аналоговым термометром (Troyka-модуль)
#include <TroykaThermometer.h>
// создаём объект для работы с аналоговым термометром
// и передаём ему номер пина выходного сигнала
TroykaThermometer thermometer(A0);

void setup()
{
  // открываем последовательный порт
  Serial.begin(9600);
  pinMode(7, OUTPUT);
}

void loop()
{
  // считываем данные с аналогового термометра
  thermometer.read();
  // вывод показателей аналогового термометра в градусах Цельсия
  Serial.print("Temperature is ");
  Serial.print(thermometer.getTemperatureC());
  Serial.println(" C");
  int temp = thermometer.getTemperatureC();
  if(temp > 15){
    digitalWrite(7, HIGH);
  }
  else{
    digitalWrite(7, LOW);
  }
  

  delay(1000);
}
```
## Display
```
#include <TroykaThermometer.h>
#include <QuadDisplay2.h>
TroykaThermometer thermometer(A0);
QuadDisplay qd(9);
void setup()
{
  // открываем последовательный порт
  Serial.begin(9600);
  qd.begin();
  pinMode(7, OUTPUT);
}

void loop()
{
  // считываем данные с аналогового термометра
  thermometer.read();
  // вывод показателей аналогового термометра в градусах Цельсия
  Serial.print("Temperature is ");
  Serial.print(thermometer.getTemperatureC());
  Serial.println(" C");

  qd.displayTemperatureC(thermometer.getTemperatureC());
  delay(1000);
}
```
## Mix
```C++
#include <TroykaThermometer.h>
#include <QuadDisplay2.h>
#define NOISE_PIN A0
TroykaThermometer thermometer(A0);
QuadDisplay qd(9);
void setup()
{
  // открываем последовательный порт
  Serial.begin(9600);
  qd.begin();
  pinMode(A0, OUTPUT);
}

void loop()
{
  int valNoise = analogRead(NOISE_PIN);
  Serial.println(valNoise);
  thermometer.read();
  Serial.print("Temperature is ");
  Serial.print(thermometer.getTemperatureC());
  Serial.println(" C");
  int temp = thermometer.getTemperatureC();
  if (temp > 15 && valNoise < 19){
    qd.displayDigits(QD_b, QD_a, QD_d, QD_NONE);
  }
  else{
    qd.displayDigits(QD_c, QD_o, QD_o, QD_d);
  }
  
}
```
