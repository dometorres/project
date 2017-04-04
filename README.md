# project
#include <LiquidCrystal.h>

#include <dht.h>

dht DHT;
LiquidCrystal lcd(12,11,5,4,3,2); //Declaramos la variable LCD y establecemos los pins que utilizaremos
#define DHT11_PIN 7

       float temp, hum; // Valor de hum y temp del sensor
       int Tmax; // Temperatura maxima
       int Tmin; // Temperatura minima
       int Hmax; // Humedad maxima
       int Hmin; // Humedad minima
      
void setup() {

Serial.begin(9600);
lcd.begin(16,2); //Establecemos la medida de la pantalla (16 espacio en eje X y 2 espacios en eje Y)
//lcd.print("hello, world!");
//lcd.setCursor(0,1);
//lcd.print("LCD funciona");

pinMode(13, OUTPUT); // Define la salida del LED
digitalWrite(13,LOW); // LED inicialmente apagado

//temp=20;
//hum=20;
Hmax=60; // Definimos humedad maxima
Hmin=40; // Definimos humedad minima
Tmax=20; // Definimos temperatura maxima
Tmin=10; // Definimos temperatura minima

}

void loop() {

int chk = DHT.read11(DHT11_PIN);

lcd.clear();
lcd.setCursor(0,0); //Empezamos a imprimir en la fila 0 posición 0
lcd.print("Temp.: "); //Escribimos temperatura
lcd.print(DHT.temperature);
lcd.print(" C");

lcd.setCursor(0,2); //Empezamos a imprimir en la segunda final posición 0
lcd.print("Humedad: "); //Escrivim Humitat
lcd.print(DHT.humidity);
lcd.print(" %");

if((DHT.temperature>Tmax)||(DHT.humidity>Hmax)){ // Si la temperatura > a Tmax o humedad > Hmax --> Se enciende el LED
  digitalWrite(13,HIGH);
}else{ //sino
  if((DHT.temperature<Tmin)||(DHT.humidity<Hmin)){//Si temperatura < Tmin o humedad < Hmin menor --> Se enciende el LED
    digitalWrite(13,HIGH);
  }else{ //sino se apaga el LED
    digitalWrite(13,LOW);
  }
}

Serial.print("Temperatura = ");

  Serial.print(DHT.temperature);
  Serial.print(" C");
  Serial.print("  Humedad = ");
  
  Serial.print(DHT.humidity);
  Serial.println(" %");
  delay(1000); //Leemos cada segundo.
}

       
