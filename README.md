# interfaz 2
### ejercicio n°1 Arduino: "Hola mundo!"

```js
void setup() {
  Serial.begin(9600); // Inicia la comunicación serie a 9600 bps
  Serial.println("Hola, Mundo!"); // Envía "Hola, Mundo!" al monitor serie
}

void loop() {
  // No es necesario poner nada en el loop para este ejemplo
}
```

### Ejercicio n°2 Arduino: "Led Parpadeante"

```js
void setup() {  // Configuración inicial (ej: pines como entrada/salida)
  pinMode(13, OUTPUT);  // Pin 13 como salida
  pinMode(8, OUTPUT);
}

void loop() {   // Se repite infinitamente
  digitalWrite(13, HIGH);  // Encender LED
  delay(1000);             // Esperar 1 segundo
  digitalWrite(13, LOW);   // Apagar LED
  //delay(1000);             // Esperar 1 segundo
  digitalWrite(8, HIGH);  // Encender LED
  delay(1000);             // Esperar 1 segundo
  digitalWrite(8, LOW);   // Apagar LED
  //delay(1000);             // Esperar 1 segundo
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/led%20parpadeante.png"
 />


### Ejercicio n°3 Arduino: "Control pulsador"

```js
void setup() {
  pinMode(2, INPUT);  // Botón como entrada
  pinMode(13, OUTPUT);
}
void loop() {
  if (digitalRead(2) == HIGH) {  // Si se presiona el botón
    digitalWrite(13, HIGH); //se prende el led
  } else { //si se suelta
    digitalWrite(13, LOW); //se apaga
  }
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/control%20pulsador.png"
 />


### Ejercicio n°4 Arduino: "Potenciometro"

```js
void setup() {
  pinMode(9, OUTPUT);  // Pin PWM (símbolo ~)
}
void loop() {
  int valor = analogRead(A0);           // Leer potenciómetro (0-1023)
  int brillo = map(valor, 0, 1023, 0, 255);  // Convertir a rango PWM
  analogWrite(9, brillo);               // Ajustar brillo
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/potenciometro.png"
 />



### ejercicio n°5 Arduino: "Semáforo"

```js
// C++ code - Semáforo Autos y Peatones

// Definición de pines
int LED_1 = 6;  // Luz roja autos
int LED_2 = 7;  // Luz amarilla autos
int LED_3 = 8;  // Luz verde autos
int LED_4 = 9;  // Luz verde peatones
int LED_5 = 10; // Luz roja peatones

void setup() {
  // Configuramos todos los pines como salida
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  pinMode(LED_3, OUTPUT);
  pinMode(LED_4, OUTPUT);
  pinMode(LED_5, OUTPUT);
}

void loop() {
  // 🚦 Fase 1: Autos en verde, peatones en rojo
  digitalWrite(LED_1, LOW);   // Rojo autos apagado
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado
  digitalWrite(LED_3, HIGH);  // Verde autos encendido
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 2: Amarillo autos, peatones siguen en rojo
  digitalWrite(LED_3, LOW);   // Verde autos apagado
  digitalWrite(LED_2, HIGH);  // Amarillo autos encendido
  delay(2000); // 2 segundos
  digitalWrite(LED_2, LOW);   // Amarillo autos apagado

  // 🚦 Fase 3: Rojo autos, verde peatones
  digitalWrite(LED_1, HIGH);  // Rojo autos encendido
  digitalWrite(LED_5, LOW);   // Rojo peatones apagado
  digitalWrite(LED_4, HIGH);  // Verde peatones encendido
  delay(5000); // 5 segundos

  // 🚦 Fase 4: Rojo autos, rojo peatones (tiempo intermedio)
  digitalWrite(LED_4, LOW);   // Verde peatones apagado
  digitalWrite(LED_5, HIGH);  // Rojo peatones encendido
  //delay(2000); // 2 segundos
}

```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/semaforo.png"
 />

### ejercicio n°6 Arduino y processing "Potenciometro"

## codigo arduino
```js
unsigned int ADCValue;
void setup(){
    Serial.begin(9600);
}

void loop(){

 int val = analogRead(0);
   val = map(val, 0, 300, 0, 255);
    Serial.println(val);
delay(50);
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/potenciador%20arduino.png"
 />
## Codigo processing
import processing.serial.*;

Serial myPort;  // Crear objeto de la clase Serial
static String val;    // Datos recibidos desde el puerto serial
int sensorVal = 0;

void setup()
{
  //background(0); 
  //fullScreen(P3D);
   size(1080, 720);
   noStroke();
  noFill();
  String portName = "COM4";// Cambia el número (en este caso) para que coincida con el puerto correspondiente conectado a tu Arduino. 

  //myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  myPort = new Serial(this, Serial.list()[0], 9600);

}

void draw()
{
  if ( myPort.available() > 0) {  // Si hay datos disponibles,
  val = myPort.readStringUntil('\n'); 
  try {
   sensorVal = Integer.valueOf(val.trim());
  }
  catch(Exception e) {
  ;
  }
  println(sensorVal); // léelos y guárdalos en vals!
  }  
 //background(0);
  // Escala el valor de mouseX de 0 a 640 a un rango entre 0 y 175
  float c = map(sensorVal, 0, width, 0, 400);
  // Escala el valor de mouseX de 0 a 640 a un rango entre 40 y 300
  float d = map(sensorVal, 0, width, 40,500);
  fill(255, c, 0);
  ellipse(width/2, height/2, d, d); 
  ellipse(width/3, height/2, d, d);
  ellipse(width/1.5, height/2, d, d);
}
```
<img src="file:///C:/Users/Maichaiil/Downloads/processing.png"
 />





