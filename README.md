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
 <img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/led%20parpadeante%202.jpg"
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
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/potenci%C3%B3metro%204.jpg"
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
 <img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/sem%C3%A1foro%20fi.jpg"
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
```
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
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/processing.png"
 />
 <img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/potenci%C3%B3metro%20process.jpg"
 />
 ### Ejercicio N°7 Arduino+Processing: "Pulsador"
 ```js
int buttonPin = 2;  // Pin del botón
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Botón con resistencia interna
  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {   // Botón presionado
    Serial.println(1);        // Enviar un "1" a Processing
    delay(200);               // Evitar rebotes
  }
}
```
### Ejercicio N°8 Arduino+Processing: "Pulsador+Potenciometro"
```js
import processing.serial.*;

Serial myPort;
ArrayList<PVector> circles; 

void setup() {
  size(1920, 1080);
  background(100);
  
  // Ajusta el nombre del puerto según tu Arduino
  println(Serial.list());
  //myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  myPort = new Serial(this, Serial.list()[0], 9600);
  
  circles = new ArrayList<PVector>();
}

void draw() {
  //background(0);
  
  // Dibujar círculos almacenados
  fill(0, 0, 0);
  //noStroke();
  stroke(0, 150, 155);
  for (PVector c : circles) {
    ellipse(c.x, c.y, 100, 5);
  }
  
  // Revisar si llega algo de Arduino
  if (myPort.available() > 0) {
    String val = myPort.readStringUntil('\n');
    if (val != null) {
      val = trim(val);
      if (val.equals("1")) {
        // Cada vez que se aprieta el botón, agregar un círculo en posición aleatoria
        circles.add(new PVector(random(width), random(height)));
      }
    }
  }
}
```
### Ejercicio N°9 Arduino: "If/Else"
```js
int buttonPin = 2;  // Pin del botón
int buttonState = 0;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP); // Botón con resistencia interna
  Serial.begin(9600);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {   // Botón presionado
    Serial.println(1);        // Enviar un "1" a Processing
    delay(200);               // Evitar rebotes
  }
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/ifelse.png.png"
 />

### Ejercicio N°10 Processing: "Botonera"
```js
// Importamos librería para comunicación serial
import processing.serial.*;
// Importamos librería Minim para manejar audio
import ddf.minim.*;

// Declaramos el objeto serial para comunicarnos con Arduino
Serial myPort;
// Objeto principal de Minim
Minim minim;
// Array de reproductores de audio (3 pistas)
AudioPlayer[] players;
// Variable para guardar el índice de la pista que está sonando
int currentTrack = -1;  // -1 significa que no hay pista activa al inicio

void setup() {
  size(400, 200); // Ventana de 400x200 píxeles
 
  // --- Configuración del puerto serial ---
  printArray(Serial.list()); // Muestra en consola la lista de puertos disponibles
  myPort = new Serial(this, Serial.list()[0], 9600); // Abrimos el primer puerto de la lista a 9600 baudios
 
  // --- Configuración de audio ---
  minim = new Minim(this); // Inicializamos Minim
  players = new AudioPlayer[3]; // Creamos un array de 3 reproductores
 
  // Cargamos los 3 archivos de audio desde la carpeta "data"
  players[0] = minim.loadFile("1.mp3", 2048);
  players[1] = minim.loadFile("2.mp3", 2048);
  players[2] = minim.loadFile("3.mp3", 2048);
}

void draw() {
  background(0); // Fondo negro
  fill(255);     // Color blanco para el texto
  textSize(16);  // Tamaño del texto
 
  // Mostramos en pantalla qué botón está activo
  text("Botón actual: " + (currentTrack == -1 ? "ninguno" : currentTrack), 20, 40);
}

void serialEvent(Serial myPort) {
  // Leemos la cadena que llega desde Arduino hasta el salto de línea
  String inString = trim(myPort.readStringUntil('\n'));
 
  // Si no llega nada, salimos
  if (inString == null) return;

  // --- Si el mensaje recibido empieza con "B" significa que es un botón ---
  if (inString.startsWith("B")) {
    // Quitamos la letra "B" y separamos el mensaje en partes (ejemplo "0:0")
    String[] parts = split(inString.substring(1), ':');
   
    // Si realmente recibimos dos partes (índice y estado)
    if (parts.length == 2) {
      int buttonIndex = int(parts[0]); // Número del botón (0,1,2)
      int state = int(parts[1]);       // Estado del botón (0 = presionado, 1 = suelto)
     
      // Si el botón fue presionado (LOW = 0 en Arduino)
      if (state == 0) {
        playTrack(buttonIndex); // Llamamos a la función para reproducir la pista correspondiente
      }
    }
  }
}

// --- Función que reproduce una pista según el botón ---
void playTrack(int index) {
  // Si ya había una pista sonando, la pausamos y la rebobinamos al inicio
  if (currentTrack != -1 && players[currentTrack].isPlaying()) {
    players[currentTrack].pause();
    players[currentTrack].rewind();
  }
 
  // Reproducimos en bucle la pista seleccionada
  players[index].loop();
 
  // Actualizamos la variable para saber cuál es la pista activa
  currentTrack = index;
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/botonera1.png"
 />

<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/botonera.jpg"
 />
 ### Ejercicio Personal arduino
 ```js
// Pines de los potenciometros
const int pot1 = A0;
const int pot2 = A1;

// Pines de los LEDs
const int led1 = 2;
const int led2 = 4;
const int led3 = 3;
const int led4 = 5;

void setup() {
  // Configuramos pines como salida
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);
}

void loop() {
  // Leemos valores de los potenciometros (0 a 1023)
  int valPot1 = analogRead(pot1);
  int valPot2 = analogRead(pot2);

  // Convertimos a rango PWM (0 a 255)
  int brillo1 = map(valPot1, 0, 1023, 0, 255);
  int brillo2 = map(valPot2, 0, 1023, 0, 255);

  // Aplicamos el brillo con PWM
  analogWrite(led1, brillo1);
  analogWrite(led2, brillo1);

  analogWrite(led3, brillo2);
  analogWrite(led4, brillo2);
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/Captura%20de%20pantalla%202025-10-07%20114034.png"
 />
 <img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/1000102739.jpg"
 />

 ### Ejercicio 11 Processing: "video Ascii"
 ```js
import processing.video.*;

Capture cam;
String asciiChars = "@%#*+=-:. ";  // Characters from dark to light
int cols, rows;
int cellSize = 10; // Size of each ASCII cell

void setup() {
  size(640, 480);
  cam = new Capture(this, 640, 480);
  cam.start();
  textAlign(CENTER, CENTER);
  textSize(cellSize);
  cols = width / cellSize;
  rows = height / cellSize;
}

void draw() {
  if (cam.available() == true) {
    cam.read();
  }

  cam.loadPixels();
  background(0);

  for (int y = 0; y < rows; y++) {
    for (int x = 0; x < cols; x++) {
      int pixelX = x * cellSize;
      int pixelY = y * cellSize;
      int index = pixelX + pixelY * cam.width;
      color c = cam.pixels[index];
      
      // Calculate brightness and map it to ASCII characters
      float bright = brightness(c);
      int charIndex = int(map(bright, 0, 255, asciiChars.length() - 1, 0));
      String asciiChar = asciiChars.substring(charIndex, charIndex + 1);

      fill(255);
      text(asciiChar, pixelX + cellSize * 0.5, pixelY + cellSize * 0.5);
    }
  }
}
}
```
### Ejercicio 12 Arduino: "Video Glitch"
```js
void setup() {
  Serial.begin(9600);
}

void loop() {
  int pot1 = analogRead(A0);  // Read first potentiometer
  int pot2 = analogRead(A1);  // Read second potentiometer

  // Send potentiometer values as comma-separated values
  Serial.print(pot1);
  Serial.print(",");
  Serial.println(pot2);
  
  delay(50);  // Delay to reduce data rate
}
```
### Ejercicio 13 Arduino: "Sensor de humedad"
```js
void setup() {
  Serial.begin(9600);
}

void loop() {
  int pot1 = analogRead(A0);  // Read first potentiometer
  int pot2 = analogRead(A1);  // Read second potentiometer

  // Send potentiometer values as comma-separated values
  Serial.print(pot1);
  Serial.print(",");
  Serial.println(pot2);
  
  delay(50);  // Delay to reduce data rate
}
```
### Ejercicio 14 arduino+processing: "cuerpo, video, sensor sharp"
```js
// --- Sensor Sharp conectado al pin A0 ---
int sensorPin = A0;
int valor;

void setup() {
  Serial.begin(9600);
}

void loop() {
  valor = analogRead(sensorPin);
  Serial.println(valor);
  delay(50); // envío cada 50 ms
}
```
#### Codigo processing
```js
// --- Librerías necesarias ---
import processing.serial.*;
import processing.video.*;

// --- Variables de cámara y serial ---
Capture cam;
Serial myPort;

// --- Variables del sensor ---
float sensorValue = 0;
float suavizado = 0;

// --- Parámetros para detección de silueta ---
float umbral = 100; // controla el contraste para definir la silueta

void setup() {
  size(1280, 720);
  background(0);
  
  // --- Inicializar cámara ---
  String[] cameras = Capture.list();
  if (cameras.length == 0) {
    println("No se encontró cámara.");
    exit();
  } else {
    println("Cámara encontrada: " + cameras[0]);
    cam = new Capture(this, cameras[0]);
    cam.start();
  }
  
  // --- Inicializar puerto serie (Arduino) ---
  // Puedes ver la lista de puertos con println(Serial.list());
  String portName = Serial.list()[0]; 
  myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  //myPort = new Serial(this, portName, 9600);
}

void draw() {
  background(0);
  
  // --- Leer datos del sensor ---
  while (myPort.available() > 0) {
    String inString = trim(myPort.readStringUntil('\n'));
    if (inString != null) {
      sensorValue = float(inString);
      suavizado = lerp(suavizado, sensorValue, 0.1);
    }
  }
  
  // --- Mapear los valores del sensor ---
  float escala = map(suavizado, 0, 1023, 1.5, 0.5); // tamaño de la silueta
  float alpha = map(suavizado, 0, 1023, 255, 80);   // opacidad según distancia
  
  // --- Captura de video ---
  if (cam.available()) {
    cam.read();
  }

  // --- Dibujar silueta desde la cámara ---
  cam.loadPixels();
  loadPixels();
  
  for (int y = 0; y < cam.height; y++) {
    for (int x = 0; x < cam.width; x++) {
      int loc = x + y * cam.width;
      color c = cam.pixels[loc];
      float brillo = brightness(c);
      
      // Si el brillo es menor que el umbral, dibujamos píxel blanco (silueta)
      if (brillo < umbral) {
        int px = int(x * escala);
        int py = int(y * escala);
        if (px < width && py < height) {
          stroke(255, alpha);
          point(px, py);
        }
      }
    }
  }
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/ejercicio%20sensor%20sharp1.png"
 />
 <img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/arduino%20sensor%20sharp.jpg"
 />
### Ejercicio 15 arduino+processing: Promedio imagenes
```js
void setup() {
  Serial.begin(9600);
}

void loop() {
  int potValue = analogRead(A0);
  Serial.println(potValue);
  delay(20);
}
```
#### codigo processing
```js
import processing.serial.*;

Serial myPort;
PImage[] imgs;
int numImages = 3;
PImage avgImg;
float mixAmount = 0;

void setup() {
  size(800, 600);
  println(Serial.list());
  
  //Cambia el índice según tu puerto (0, 1, 2, etc.)
  myPort = new Serial(this, Serial.list()[0], 9600);
  //myPort = new Serial(this, "/dev/cu.usbmodem1101", 9600);
  myPort.bufferUntil('\n');

  // Cargar imágenes
  imgs = new PImage[numImages];
  imgs[0] = loadImage("img1.jpg");
  imgs[1] = loadImage("img2.jpg");
  imgs[2] = loadImage("img3.jpg");

  avgImg = createImage(imgs[0].width, imgs[0].height, RGB);
}

void draw() {
  // Dibujar la imagen promedio según el valor del potenciómetro
  background(0);
  calcAverage(mixAmount);
  image(avgImg, 0, 0, width, height);
  
  fill(255);
  textSize(20);
  text("Mezcla: " + nf(mixAmount, 1, 2), 20, height - 20);
}

void serialEvent(Serial p) {
  String val = p.readStringUntil('\n');
  if (val != null) {
    val = trim(val);
    float sensor = float(val);
    mixAmount = map(sensor, 0, 1023, 0, 1); // 0 a 1
  }
}

void calcAverage(float t) {
  avgImg.loadPixels();

  for (int i = 0; i < avgImg.pixels.length; i++) {
    color c1 = imgs[0].pixels[i];
    color c2 = imgs[1].pixels[i];
    color c3 = imgs[2].pixels[i];

    // Promedio ponderado según el potenciómetro
    float r = red(c1)*(1-t) + red(c2)*t*0.5 + red(c3)*t*0.5;
    float g = green(c1)*(1-t) + green(c2)*t*0.5 + green(c3)*t*0.5;
    float b = blue(c1)*(1-t) + blue(c2)*t*0.5 + blue(c3)*t*0.5;

    avgImg.pixels[i] = color(r, g, b);
  }
  avgImg.updatePixels();
}
```
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/imagenes%20ejercicio.png"
 />
<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/ejercicio%20imagenes.jpg"
 />

### Ejercicio 17: proyecto "Espacio entre texturas"
#### Alumnas Jacqueline Peralta, Sofia Salazar, Javiera Leon
```
El proyecto "Espacio entre Texturas" nace desde nuestros intereses en común; la botánica y la astronomía como dos opuestos
que se pueden relacionar y a su vez el uso del cuerpo humano como una herramienta que "controla"
a través del sensor sharp estas dos facetas para crear una conexión entre lo micro y lo macro, lo natural y el universo.

Nuestro objetivo es crear un juego de texturas relacionados a estos dos campos:
Desde una mirada tanto de lo micro, donde se utilizan gofrados e impresiones que simulan raíces y lo relacionado a la tierra.
Como una mirada desde lo macro, utilizando renderizados de nebulosas y lo relacionado al universo.
```
#### Codigo arduino
```
void setup() {
  Serial.begin(9600);  // Inicializamos la comunicación serial
}

void loop() {
  int sensorValue = analogRead(A0);  // Leemos el valor del sensor Sharp (valor analógico entre 0 y 1023)
  Serial.println(sensorValue);  // Enviamos el valor leído al puerto serial
  delay(50);  // Espera de 20 ms
}
```
#### Codigo Processing
```
// --- Librerías necesarias ---
import processing.serial.*;

// --- Comunicación serial con Arduino ---
Serial myPort;
float sensorValue = 0;

// --- Variables de imágenes ---
PImage[] imgs;   // Arreglo para 30 imágenes
PImage avgImg;   // Imagen resultante

// --- Configuración inicial ---
void setup() {
  fullScreen();  // Tamaño de ventana

  // --- Cargar las 30 imágenes PNG nombradas del 1 al 30 ---
  imgs = new PImage[30];
  for (int i = 0; i < imgs.length; i++) {
    String filename = "imagenes/" + (i + 1) + ".png"; // 1.png a 30.png
    imgs[i] = loadImage(filename);
    if (imgs[i] == null) {
      println("No se pudo cargar: " + filename);
    } else {
      imgs[i].resize(width, height); // Ajustar tamaño a la ventana
      println("Cargada: " + filename);
    }
  }

  avgImg = createImage(width, height, RGB); // Imagen mezclada

  // --- Conectar con Arduino ---
  printArray(Serial.list()); // Mostrar puertos disponibles
  // Ajusta el índice o nombre del puerto si es necesario:
  myPort = new Serial(this, Serial.list()[0], 9600);
}

// --- Bucle principal ---
void draw() {
  background(0);

  // Leer valor del sensor Sharp
  readSerial();

  // Mapear (0–1023) al rango de las 30 imágenes (0–29)
  float mixValue = map(sensorValue, 0, 1023, 0, imgs.length - 1);

  // Mezclar imágenes según el valor leído
  avgImagesWeighted(mixValue);

  // Mostrar imagen resultante
  image(avgImg, 0, 0);

  // Mostrar información en pantalla
  fill(255);
  textSize(20);
  text("Valor sensor: " + nf(sensorValue, 1, 0), 10, height - 40);
  text("Imagen mezclada: " + nf(mixValue, 1, 2), 10, height - 15);
}

// --- Función de mezcla entre imágenes ---
void avgImagesWeighted(float mix) {
  avgImg.loadPixels();

  mix = constrain(mix, 0, imgs.length - 1);

  int i1 = floor(mix);                   // Imagen base
  int i2 = min(i1 + 1, imgs.length - 1); // Imagen siguiente
  float t = mix - i1;                    // Fracción entre ambas

  imgs[i1].loadPixels();
  imgs[i2].loadPixels();

  for (int i = 0; i < avgImg.pixels.length; i++) {
    color c1 = imgs[i1].pixels[i];
    color c2 = imgs[i2].pixels[i];

    float r = lerp(red(c1), red(c2), t);
    float g = lerp(green(c1), green(c2), t);
    float b = lerp(blue(c1), blue(c2), t);

    avgImg.pixels[i] = color(r, g, b);
  }

  avgImg.updatePixels();
}

// --- Lectura del puerto serial ---
void readSerial() {
  while (myPort.available() > 0) {
    String val = myPort.readStringUntil('\n');
    if (val != null) {
      val = trim(val);
      if (val.length() > 0) {
        sensorValue = float(val);
      }
    }
  }
}

```
[<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/espacio%20entre%20texturas.png"
 />
[<img src="https://raw.githubusercontent.com/jake11401/interfaz2/refs/heads/main/Img/EET%20exper.jpg"
 />
[<img src="https://github.com/jake11401/interfaz2/blob/main/Img/EET%20caja.jpg"
 />

 







