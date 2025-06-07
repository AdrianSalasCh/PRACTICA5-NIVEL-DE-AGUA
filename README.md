# PRACTICA5-NIVEL-DE-AGUA
En esta practica se hará la conexión de un ESP32 con unos LED, indicando el nivel de agua que detecta un sensor HC-SR04, mostrando la información en un LCD I2C

## INTRODUCCIÓN

### DESCRIPCIÓN
La ESP32 la utilizamos en un entorno de adquision de datos, lo cual en esta practica ocuparemos un sensor ultrasónico (HC-SR04) para adquirir la distancia y medir el nivel de agua en un contenedor y mostrar dicho nivel mediante LEDs y en una pantalla LCD; Cabe aclarar que esta practica se usara un simulador llamado WOKWI.

### MATERIAL NECESARIO

Para realizar esta practica necesitas lo siguiente
- [WOKWI](https://wokwi.com/)
- 1 PZ Tarjeta ESP 32
- 1 PZ Sensor HC-SR0 Ultrasonic Distance Sensor
- 1 PZ LCD 16x2 (I2C)
- 4 PZ LED
- 4 PZ RESISTOR
- 1 PZ GND Symbol

### INSTRUCCIONES

**REQUISITOS PREVIOS**
Para poder usar este repositorio necesitas entrar a la plataforma [WOKWI](https://wokwi.com/)

### Instrucciones de preparación de entorno

1. Abrir la terminal de programación y colocar la siguente programación:

```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 19;
const int led1 = 16;
const int led2 = 0;
const int led3 = 2;
const int led4 = 15;

#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

// defines variables
long duration;
int distance;
int safetyDistance;


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

lcd.setCursor(0, 0);
lcd.print("Diplomado");
lcd.setCursor(0, 1);
lcd.print("Automatizacion");
delay (2000);
lcd.clear();
lcd.setCursor(0, 0);
lcd.print("Adrian Salas");
lcd.setCursor(0, 1);
lcd.print("lng Industrial");
delay (2000);
lcd.clear();
lcd.setCursor(0, 0);
lcd.print(" 07/06/2025");
delay(2000);
lcd.clear();
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
if (safetyDistance>=1 && safetyDistance<=75)
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print("LLENO");
  lcd.setCursor(0, 1);
  lcd.print("Distancia: "+ String (distance)+"cm");
  delay (2000);
  lcd.clear();
}
else if(safetyDistance>=75 && safetyDistance<=150) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print("CAPACIDAD 3/4");
  lcd.setCursor(0, 1);
  lcd.print("Distancia: "+ String (distance)+"cm");
  delay (2000);
  lcd.clear();
}
else if(safetyDistance>=150 && safetyDistance<=225) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print("CAPACIDAD 1/2");
  lcd.setCursor(0, 1);
  lcd.print("Distancia: "+ String (distance)+"cm");
  delay (2000);
  lcd.clear();
}
else if(safetyDistance>=225 && safetyDistance<=300) 
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  lcd.setCursor(0, 0);
  lcd.print("VACIO");
  lcd.setCursor(0, 1);
  lcd.print("Distancia: "+ String (distance)+"cm");
  delay (2000);
  lcd.clear();
}
else
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
  lcd.setCursor(0, 0);
  lcd.print("ERROR");
  delay (2000);
  lcd.clear();
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (2000);

}
```
2. Instalar la siguiente libreria:
      - **LiquidCrystal I2C**
   Como se muestra en la siguente imagen.

![](https://github.com/AdrianSalasCh/PRACTICA5-NIVEL-DE-AGUA/blob/main/LiquidCrystal%20I2C%20P4.PNG)

3. Hacer la conexion del HC-SR0 con la ESP32, el LCD 16x2 (I2C), los LEDs y los resistores como se muestra en la siguente imagen.

![](https://github.com/AdrianSalasCh/PRACTICA5-NIVEL-DE-AGUA/blob/main/CONEXION%20P5.PNG)

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial y en el LCD.
3. Colocar la distancia dando *doble click* al sensor **HC-SR0**

## RESULTADOS

Cuando haya funcionado, verás los valores dentro del monitor serial y en el LCD, también se iluminarán los LEDs dependiendo el nivel seleccionado, como se muestra en las siguentes imagenes.

![](https://github.com/AdrianSalasCh/PRACTICA5-NIVEL-DE-AGUA/blob/main/SIMULACI%C3%93N%20TERMINADA%20P5-1.PNG)

![](https://github.com/AdrianSalasCh/PRACTICA5-NIVEL-DE-AGUA/blob/main/SIMULACI%C3%93N%20TERMINADA%20P5-2.PNG)

![](https://github.com/AdrianSalasCh/PRACTICA5-NIVEL-DE-AGUA/blob/main/SIMULACI%C3%93N%20TERMINADA%20P5-3.PNG)

![](https://github.com/AdrianSalasCh/PRACTICA5-NIVEL-DE-AGUA/blob/main/SIMULACI%C3%93N%20TERMINADA%20P5-4.PNG)

## CRÉDITOS

Desarrollado por Ing. Luis Adrián Salas Chávez
- [GitHub](https://github.com/)
