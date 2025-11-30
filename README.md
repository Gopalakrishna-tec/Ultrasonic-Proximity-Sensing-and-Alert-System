# Ultrasonic Proximity Sensing and Alert System

A simple Arduino-based proximity alert system using the **HC-SR05 ultrasonic sensor**. It measures distance in real time and activates an **LED** and **buzzer** when objects come close. Ideal for beginners, engineering mini-projects, and basic embedded system learning.

---

## 📦 Parts List
- Arduino Uno × 1  
- HC-SR05 Ultrasonic Sensor × 1  
- LED × 1  
- Buzzer × 1  
- Jumper Wires  
- USB Programming Cable  

---

## 🔌 Connection Details

### Ultrasonic Sensor → Arduino
- VCC → 5V  
- GND → GND  
- TRIG → D9  
- ECHO → D10  

### LED → Arduino
- Anode (+) → D7  
- Cathode (–) → GND  

### Buzzer → Arduino
- + → D8  
- – → GND  

---

## 📏 Working Principle
The HC-SR05 emits ultrasonic pulses and detects the returning echo. Arduino calculates the distance:

- LED turns **ON** when distance < 20 cm  
- Buzzer turns **ON** when distance < 10 cm  
- Distance values are printed on the Serial Monitor  

---

## 💡 Arduino Code

```cpp
#define trigPin 9
#define echoPin 10
#define ledPin 7
#define buzzerPin 8

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(ledPin, OUTPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  long duration, distance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = (duration * 0.0343) / 2;

  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");

  digitalWrite(ledPin, distance < 20);
  digitalWrite(buzzerPin, distance < 10);

  delay(200);
}


