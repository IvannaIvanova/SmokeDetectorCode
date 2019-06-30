#include <Adafruit_NeoPixel.h>
#define LED_PIN 3
#define LED_COUNT 24
int sensorValue = 0;
Adafruit_NeoPixel leds
  = Adafruit_NeoPixel(LED_COUNT, LED_PIN, NEO_GRB + NEO_KHZ800);

void setup()
{
  Serial.begin(9600);
  leds.begin();
  pinMode(2, OUTPUT);
  pinMode(LED_PIN, INPUT);
  pinMode(A5, INPUT);
}

void loop()
{
  sensorValue = analogRead(A5);
 if (sensorValue >= 700) {
   Serial.println(sensorValue);
  playTone();
  showLights();
 }
  
 if(sensorValue < 700)
 {
    leds.clear();
    leds.show();
    
 }
}

void playTone(){
  tone(2, 261, 300);
  delay(400);
  tone(2, 300, 300);
  delay(400);
  }

void showLights(){
  for (int i=0; i < LED_COUNT; i++)
  { 
    leds.setPixelColor
      (i, leds.Color(255, 255, 0));
    leds.show();  
    
    leds.setPixelColor
      (i, leds.Color(255, 0, 0));
    leds.show();
  }
}
