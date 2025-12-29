// Vehicle Tracking and Accident Alert System
// Updated: Uses AltSoftSerial for GSM to avoid conflict with GPS

#include <SoftwareSerial.h>
#include <AltSoftSerial.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <Adafruit_MPU6050.h>
#include <Adafruit_Sensor.h>
#include <TinyGPS++.h>

// GPS (using SoftwareSerial)
SoftwareSerial gpsSerial(3, 2);  // GPS TX -> D3, RX -> D2
TinyGPSPlus gps;

// GSM (using AltSoftSerial for better stability)
AltSoftSerial gsmSerial; // TX = 9, RX = 8

// LCD
LiquidCrystal_I2C lcd(0x27, 16, 2);

// MPU6050
Adafruit_MPU6050 mpu;

// SW420 Vibration Sensor
#define VIBRATION_PIN 6

// Buzzer
#define BUZZER_PIN 5

// Motor Relay
#define RELAY_PIN 7

// State Flags
bool crashDetected = false;
bool rolloverDetected = false;
bool sentAlert = false;

void setup() {
  Serial.begin(9600);
  gpsSerial.begin(9600);
  gsmSerial.begin(9600);

  pinMode(VIBRATION_PIN, INPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(RELAY_PIN, OUTPUT);
  digitalWrite(RELAY_PIN, HIGH);  // Motor ON initially

  // LCD
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("System Initializing");
  delay(2000);

  // MPU6050 Init
  if (!mpu.begin()) {
    lcd.clear();
    lcd.print("MPU6050 Fail");
    while (1) delay(10);
  }
  lcd.clear();
  lcd.print("System Ready");
  delay(1000);
  lcd.clear();
}

void loop() {
  sensors_event_t a, g, temp;
  mpu.getEvent(&a, &g, &temp);

  // Detect tilt (rollover)
  float ax = a.acceleration.x;
  float ay = a.acceleration.y;
  rolloverDetected = (abs(ax) > 7 || abs(ay) > 7);

  // Detect crash
  crashDetected = digitalRead(VIBRATION_PIN);

  if ((crashDetected || rolloverDetected) && !sentAlert) {
    // Motor OFF
    digitalWrite(RELAY_PIN, LOW);

    // Buzzer ON briefly
    digitalWrite(BUZZER_PIN, HIGH);
    delay(1500);
    digitalWrite(BUZZER_PIN, LOW);

    // Display alert
    lcd.clear();
    if (crashDetected && rolloverDetected)
      lcd.print("Multi-Hazard!");
    else if (crashDetected)
      lcd.print("Crash Detected");
    else
      lcd.print("Rollover Detected");

    // Call first
    gsmSerial.println("ATD+917010041350;");
    delay(7000);  // Wait 7 sec
    gsmSerial.println("ATH"); // Hang up

    // Send SMS
    String message = "ALERT! ACCIDENT! HELP!\n";
    if (gps.location.isValid()) {
      message += "https://maps.google.com/?q=";
      message += String(gps.location.lat(), 6);
      message += ",";
      message += String(gps.location.lng(), 6);
    } else {
      message += "Location not available";
    }
    sendSMS(message);
    sentAlert = true;
  }

  // Read GPS data
  while (gpsSerial.available() > 0)
    gps.encode(gpsSerial.read());
}

void sendSMS(String msg) {
  gsmSerial.println("AT+CMGF=1");
  delay(1000);
  gsmSerial.println("AT+CMGS=\"+917010041350\"");
  delay(1000);
  gsmSerial.print(msg);
  delay(1000);
  gsmSerial.write(26); // Ctrl+Z
  delay(3000);
}
