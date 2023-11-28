## Gambaran Umum

Kode ini berfungsi untuk mengatur servo, sensor Ultrasonic, dan sensor LED pada tong sampah otomatis.
Tong sampah terbuka secara otomatis ketika ada objek didepan sensor ultrasonic (sensor gerak) dengan bantuan servo.
Kemudian sensor LED sebagai lampu indikator yang menunjukkan bahwa terdapat objek terdeteksi oleh sensor gerak.

## Bahasa Pemrograman

Kode proyek ini ditulis menggunakan bahasa pemrograman Arduino.

## Software Pendukung

Proyek ini dikembangkan menggunakan [Arduino IDE](https://www.arduino.cc/en/software).

## Alat Pendukung

1x Arduino Uno R3 Atmega328P DIP + 16U2 with Cable

1x Tower Pro Micro Servo Mini 9 Gram, 1.6Kg, 12 Sec.

1x HC-SR04 Sensor Ultrasonic Module

1x LED Blue 5mm

3x Female to Female Wire

4x Male to Female

1x Tong Sampah Manual

## Cara Penggunaan
Buka

## Preview Prototipe
Klik [tautan](https://youtu.be/ayjj4PM1EOo?si=qAO4eSFFvVy72fYW) ini untuk menonton cuplikan.

## Contoh Penggunaan Program
```ino
//define Pins
#include <Servo.h>

Servo servo;
int led = 13;
int trigPin = 9;
int echoPin = 8;

// defines variables
long duration;
int distance;

void setup() 
{
  servo.attach(7);
  servo.write(0);
  delay(2000);
  
  //Sets the Led as an Output
  pinMode(led, OUTPUT);
  // Sets the trigPin as an Output
  pinMode(trigPin, OUTPUT);
  // Sets the echoPin as an Input 
  pinMode(echoPin, INPUT);
  // Starts the serial communication 
  Serial.begin(9600); 
}

void loop() 
{
  // Clears the trigPin
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  // Sets the trigPin on HIGH state for 10 microseconds
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  // Reads the echoPin, returns the sound wave travel time in microseconds
  duration = pulseIn(echoPin, HIGH);
  // Calculating the distance
  distance= duration * 0.034 / 2;
  
  // Prints the distance on the Serial Monitor
  Serial.print("Distance: ");
  Serial.println(distance);
  
  if (distance <= 14) // Change Distance according to Ultrasonic Sensor Placement
  {
    digitalWrite(led, HIGH);
    servo.write(0);
    delay(5000);
  } 
  else if (distance <= 25) // Change Distance according to Ultrasonic Sensor Placement
  {
    digitalWrite(led, LOW);
    servo.write(90);
    delay(3000);
  } 
  else
  {
    digitalWrite(led, LOW);
    servo.write(90);
  }
}
