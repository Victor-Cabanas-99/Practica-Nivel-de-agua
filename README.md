# PRACTICA-NIVEL-DE-AGUA
## INTRODUCCION 
### Descripcion 
Con un sensor ULTRASONICO de medirá la distancia del nivel de agua de un tanque indicando el nivel en una pantalla lcd y con leds 
La Esp32 es una tarjeta de adquisición de datos, paralo cual en esta practica ocuparemos un sensor (DTH11) con una pantalla LCD216 para adquirir datos de temperatura y humedad del entorno cada segundo y mostrarlar los datos en la panatlla, se usara un simulador llamado WOKWI.
## MATERIAL A UTILIZAR
- [WOKWI](https://wokwi.com/projects/new/esp32)
- TARJET ESP32
- SENSOR ULTRASONICO
- LCD 16X2 2IC
- Relay Module
  
## INSTRUCCIONES
Insertar el codigo dado de la practica, se realizara la misma actividad que la practica anterior mostrando datos de quien esta programando:


```
// defines pins numbers
const int trigPin = 4;
const int echoPin = 15;
const int led1 = 23;
const int led2 = 17;
const int led3 = 19;
const int led4 = 18;

#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

// defines variables
long duration;
int distance;
int safetyDistance;

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
if (safetyDistance>=2 && safetyDistance<=5) //90%
{
  digitalWrite(led1, HIGH);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);

  lcd.clear(); 
  lcd.setCursor(0, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(0, 1);
  lcd.print("Mecatronica");
 delay(2000);

lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Victor Cabanas");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distance)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 90%");
  delay(2000);
}
else if(safetyDistance>=5 && safetyDistance<=10) //75%
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, HIGH);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);

  lcd.clear(); 
  lcd.setCursor(0, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(0, 1);
  lcd.print("Mecatronica");
 delay(2000);

lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Victor Cabanas");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distance)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 75%");
  delay(2000);
}
else if(safetyDistance>=11 && safetyDistance<=20) //50%
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, HIGH);
  digitalWrite(led4, HIGH);
  lcd.clear(); 
  lcd.setCursor(0, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(0, 1);
  lcd.print("Mecatronica");
 delay(2000);

lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Victor Cabanas");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distance)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 50%");
  delay(2000);
}
else if(safetyDistance>=21 && safetyDistance<=40) 
{
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, HIGH);

  lcd.clear(); 
  lcd.setCursor(0, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(0, 1);
  lcd.print("Mecatronica");
 delay(2000);

lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Victor Cabanas");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distance)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 25%");
  delay(2000);
}
else
{
 digitalWrite(led1,  LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);

  lcd.clear(); 
  lcd.setCursor(0, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(0, 1);
  lcd.print("Mecatronica");
 delay(2000);

lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Victor Cabanas");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print(" Distancia: " + String(distance)+"cm");
  lcd.setCursor(2, 1);
  lcd.print("Tanque: 0%");
  delay(2000);
}

// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
delay (2000);
}
```
2. Instalar la libreria de **LiquidCrystal I2C** como se muestra en la siguente imagen.

![]()

3. Hacer la conexion de **LCD 16X2 2IC**, el **HC-SR04 ULTRASONIC DISTANCE SENSOR**  y los **Relay Module** con la **ESP32** como se muestra en la siguente imagen.

![]()

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia *doble click* al sensor **HC-SR04 ULTRASONIC DISTANCE SENSOR**

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.
![]()
![]()
![]()
![]()
## Librerías

1. **LiquidCrystal I2C**

