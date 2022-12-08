#include "UbidotsMicroESP8266.h" #include "HX711.h" HX711 scale(D1, D0); int buz=D6; #define DEVICE1 "632c41903f4602096b56ba3c" #define TOKEN "BBFF-dXpNfSNREiluawMdTX09kpxJM6Cju6"
#define WIFISSID "Firmware" // Put here your Wi-Fi SSID #define PASSWORD "Solutions@12345" // Put here your Wi-Fi passwor Ubidots client(TOKEN); int c=100; int old=0; void setup () { Serial.begin(9600); pinMode(buz,OUTPUT); digitalWrite(buz,LOW);

Serial.print("fffff"); scale.set_scale(2280.f);
scale.tare();
client.wifiConnection(WIFISSID, PASSWORD);
}

void loop () {

int y=(scale.get_units());
{
  old=(y)*-5;
}
old= map(old, 0, 260, 0, 100);

if(old<=10&&old>2) digitalWrite(buz,HIGH); else digitalWrite(buz,LOW);

Serial.println(old);
client.add( DEVICE1, old); client.sendAll(false); delay(2000); }
