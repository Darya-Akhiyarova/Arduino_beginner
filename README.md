# Arduino_beginner
Код и схемы

## 1
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

## 2
