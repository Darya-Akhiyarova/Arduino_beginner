# Arduino_beginner
Код и схемы

## SENSORS 
```
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
## 2 Светофор
```
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

```
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
