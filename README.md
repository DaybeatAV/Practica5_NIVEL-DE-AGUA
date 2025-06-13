# Práctica 5 "NIVEL DE AGUA"
Haremos uso de componentes leds como guía visual del sensor Ultrasónico y se mostrará como un dato más en la pantalla LCD

## Introducción

### Descripción 

La pantalla LCD en este caso nos mostrará en su display el nivel de agua con uso de componentes leds como guía visual.

### Material necesario

- Software ```WOKWI```
- ```Tarjeta ESP32```
- ```Sensor ultrasonico```
- ```LCD 16x2 (I2C)```
- ```4 led (Pueden o no ser del mismo color)```
- ```4 resistencias (220 Ohms)```
- ```Símbolo GND (Tierra)```

## Instrucciones

### Requisitos previos 

Para el uso y operación de esta práctica es necesario el software ```WOKWI``` con el que ya hemos trabajado con anterioridad

### Instrucciones de prepracion de entorno

1. El primer paso será abrir la terminal de programación dentro del software e insertar las siguientes líneas de código:

```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 16;
const int led2 = 0;
const int led3 = 2;
const int led4 = 18;

// defines variables
long duration;
int distance;
int safetyDistance;
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
pinMode(led1, OUTPUT);
pinMode(led2, OUTPUT);
pinMode(led3, OUTPUT);
pinMode(led4, OUTPUT);
Serial.begin(9600); // Starts the serial communication
 lcd.init();
 lcd.backlight();
}


void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);

// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);

// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);

// Calculating the distance
distance= duration*0.034/2;

safetyDistance = distance;
if (safetyDistance>=10 && safetyDistance<=98)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
   lcd.setCursor(0, 0);
  lcd.print("Diplomado");
  lcd.setCursor(0, 1);
  lcd.print("Automatizacion");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Irving Cardoso");
  lcd.setCursor(0, 1);
  lcd.print("Ing Mecanica");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("  07/06/2025");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
  lcd.print("Nivel 1/4");
  delay(2000);          
  lcd.clear();
}
else if(safetyDistance>=99 && safetyDistance<=198) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
     lcd.setCursor(0, 0);
  lcd.print("Diplomado");
  lcd.setCursor(0, 1);
  lcd.print("Automatizacion");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Irving Cardoso");
  lcd.setCursor(0, 1);
  lcd.print("Ing Mecanica");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("  07/06/2025");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
  lcd.print("Nivel 1/2");
  delay(2000);          
  lcd.clear();
}
else if (safetyDistance>=199 && safetyDistance<=298) 
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
     lcd.setCursor(0, 0);
  lcd.print("Diplomado");
  lcd.setCursor(0, 1);
  lcd.print("Automatizacion");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Irving Cardoso");
  lcd.setCursor(0, 1);
  lcd.print("Ing Mecanica");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("  07/06/2025");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
  lcd.print("Nivel 3/4");
  delay(2000);          
  lcd.clear();
}
else if (safetyDistance>=299 && safetyDistance<=398) 
{
 digitalWrite(led1,  HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
     lcd.setCursor(0, 0);
  lcd.print("Diplomado");
  lcd.setCursor(0, 1);
  lcd.print("Automatizacion");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Irving Cardoso");
  lcd.setCursor(0, 1);
  lcd.print("Ing Mecanica");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("  07/06/2025");
  delay (2000);
  lcd.clear();
  lcd.setCursor(0,0);
  lcd.print("Distancia: "+ String (distance)+"cm");
  lcd.setCursor(0,1);
  lcd.print("Nivel lleno");
  delay(2000);          
  lcd.clear();
}
// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (2000);
}
```
2. Después procederemos a instalar la librería ```LiquidCrystal I2C``` como se observa aqui debajo:

![]()

3. A continuación vamos insertar y después haremos la conexión del componente ```HC-SR04 ULTRASONIC Distance sensor``` con la tarjeta ```ESP32```:

![]()

4. Procederemos a crear la conexion entre la pantalla ```LCD I2C``` con la tarjeta ```ESP32```:

![]()


## Instrucciones de operacion
1. El primer pasó será ejecutar el software de simulación ```WOKWI```

2. Después se tendrán que observar los datos en la pantalla LCD (I2C) cada cierto intervalo de tiempo

3. Lo siguiente será variar la distancia dando doble click al sensor Ultrasonico para darle distintos valores y ver el cambio

4. Por último deberemos declarar con antelación las condiciones de distancia que se dieron en el código principal, por lo cuál irán encenciendo los leds y se mostrará en la pantalla el valor del nivel a la par

## Resultados
Cuando haya funcionado el display te mandará las siguientes imagenes en retardos de dos segundos

![]()

![]()

![]()

![]()

## Créditos
Creado y desarrollado por **JOSE DAVID AYALA VILLALBA**

-[GITHUB](https://github.com/DaybeatAV)
