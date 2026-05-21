#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include "RTClib.h"
#include <WiFi.h>
#include <WebServer.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);
RTC_DS3231 rtc;

// WiFi (use your hotspot/router)
const char* ssid = "ESP32";
const char* password = "12345678";

WebServer server(80);

// LEDs
int redLED = 27;
int blueLED = 14;
int greenLED = 12;

int buzzer = 13;

// Buttons
int setBtn = 32;
int incBtn = 33;
int okBtn  = 25;

// Alarm minutes
int m1 = 1, m2 = 2, m3 = 3;

int mode = 0;
int box = 1;

// Status
bool taken1 = false;
bool taken2 = false;
bool taken3 = false;

int activeBox = 0;
bool alarmTriggered = false;

// 🌐 Web Page (VIEW ONLY)
void handleRoot() {
  DateTime now = rtc.now();

  String html = "<!DOCTYPE html><html><head>";
  html += "<meta charset='UTF-8'>";
  html += "<meta name='viewport' content='width=device-width, initial-scale=1'>";
  html += "<meta http-equiv='refresh' content='2'/>";

  html += "<style>";
  html += "body{font-family:Arial;background:#0f172a;color:white;text-align:center;margin:0;}";
  html += ".container{padding:20px;}";
  html += ".title{font-size:28px;margin-bottom:10px;}";
  html += ".time{font-size:40px;margin:20px 0;color:#38bdf8;}";
  html += ".card{background:#1e293b;margin:10px auto;padding:15px;border-radius:12px;width:80%;max-width:300px;}";
  html += ".taken{color:#22c55e;font-weight:bold;}";
  html += ".not{color:#ef4444;font-weight:bold;}";
  html += "</style>";

  html += "</head><body><div class='container'>";
  html += "<div class='title'>Medicine Reminder</div>";

  html += "<div class='time'>";
  html += String(now.hour()) + ":" + String(now.minute());
  html += "</div>";

  // Box 1
  html += "<div class='card'><h3>Box 1</h3>";
  html += "<p class='" + String(taken1 ? "taken" : "not") + "'>";
  html += taken1 ? "Taken" : "Not Taken";
  html += "</p></div>";

  // Box 2
  html += "<div class='card'><h3>Box 2</h3>";
  html += "<p class='" + String(taken2 ? "taken" : "not") + "'>";
  html += taken2 ? "Taken" : "Not Taken";
  html += "</p></div>";

  // Box 3
  html += "<div class='card'><h3>Box 3</h3>";
  html += "<p class='" + String(taken3 ? "taken" : "not") + "'>";
  html += taken3 ? "Taken" : "Not Taken";
  html += "</p></div>";

  html += "</div></body></html>";

  server.send(200, "text/html", html);
}

void setup() {
  Serial.begin(115200);

  Wire.begin(21, 22);
  lcd.init();
  lcd.backlight();
  rtc.begin();

  pinMode(redLED, OUTPUT);
  pinMode(blueLED, OUTPUT);
  pinMode(greenLED, OUTPUT);
  pinMode(buzzer, OUTPUT);

  pinMode(setBtn, INPUT_PULLUP);
  pinMode(incBtn, INPUT_PULLUP);
  pinMode(okBtn, INPUT_PULLUP);

  // WiFi
  WiFi.mode(WIFI_STA);
  WiFi.disconnect(true);
  delay(1000);

  WiFi.begin(ssid, password);

  lcd.print("Connecting WiFi");

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  lcd.clear();
  lcd.print("IP:");
  lcd.setCursor(0,1);
  lcd.print(WiFi.localIP());

  server.on("/", handleRoot);
  server.begin();

  delay(2000);
  lcd.clear();
}

void loop() {
  server.handleClient();

  DateTime now = rtc.now();

  // Enter setting mode
  if (digitalRead(setBtn) == LOW) {
    delay(250);
    mode = 1;
    box = 1;
    lcd.clear();
  }

  // Setting mode
  if (mode == 1) {
    lcd.setCursor(0,0);
    lcd.print("Set Box ");
    lcd.print(box);

    lcd.setCursor(0,1);
    if (box == 1) lcd.print(m1);
    if (box == 2) lcd.print(m2);
    if (box == 3) lcd.print(m3);

    if (digitalRead(incBtn) == LOW) {
      if (box == 1) m1 = (m1 + 1) % 60;
      if (box == 2) m2 = (m2 + 1) % 60;
      if (box == 3) m3 = (m3 + 1) % 60;
      delay(250);
      lcd.clear();
    }

    if (digitalRead(okBtn) == LOW) {
      delay(250);
      box++;
      if (box > 3) mode = 0;
      lcd.clear();
    }
    return;
  }

  // Display
  lcd.setCursor(0,0);
  lcd.print("Time:");
  lcd.print(now.hour());
  lcd.print(":");
  lcd.print(now.minute());

  lcd.setCursor(0,1);
  lcd.print("1:");
  lcd.print(taken1 ? "T " : "NT");
  lcd.print("2:");
  lcd.print(taken2 ? "T " : "NT");
  lcd.print("3:");
  lcd.print(taken3 ? "T" : "NT");

  // Reset outputs
  digitalWrite(redLED, LOW);
  digitalWrite(blueLED, LOW);
  digitalWrite(greenLED, LOW);
  noTone(buzzer);

  // Alarm logic
  if (now.minute() == m1 && now.second() < 10) {
    if (!alarmTriggered) {
      activeBox = 1;
      taken1 = false;
      alarmTriggered = true;
    }
    digitalWrite(redLED, HIGH);
    tone(buzzer, 1000);
  }

  if (now.minute() == m2 && now.second() < 10) {
    if (!alarmTriggered) {
      activeBox = 2;
      taken2 = false;
      alarmTriggered = true;
    }
    digitalWrite(blueLED, HIGH);
    tone(buzzer, 1200);
  }

  if (now.minute() == m3 && now.second() < 10) {
    if (!alarmTriggered) {
      activeBox = 3;
      taken3 = false;
      alarmTriggered = true;
    }
    digitalWrite(greenLED, HIGH);
    tone(buzzer, 1500);
  }

  if (now.second() > 10) {
    alarmTriggered = false;
  }

  // OK button
  if (mode == 0 && digitalRead(okBtn) == LOW) {

    if (activeBox == 1) taken1 = true;
    if (activeBox == 2) taken2 = true;
    if (activeBox == 3) taken3 = true;

    noTone(buzzer);
    digitalWrite(redLED, LOW);
    digitalWrite(blueLED, LOW);
    digitalWrite(greenLED, LOW);

    delay(300);
  }

  delay(200);
}