APUNTES: (11/abril)

Integrantes: Martin Gonzales, Mauricio Viveros y Valentina Tiznado

Serialwrite: envia mensajes que no llegan a la consola, hay que recibirlos

Codigo Processing (Ejemplo de clases)

void setup ()
{
  size(400, 400);
}

void draw()
{
  background(220);
  
  fill(100, 255, 4);
  rect(25, 25, 250, 250);
  noStroke();
}

Trabajamos con el programa Processing y Arduino IDE, donde debiamos enviar uno de los ejemplos que trae Processing, especificamente con SimpleRead. Donde al apretar un boton debia pasar de un cuadrado negro a uno grus, ocupamos el siguente codigo;

- Codigo Porcessing:
**
 * Simple Read
 * 
 * Read data from the serial port and change the color of a rectangle
 * when a switch connected to a Wiring or Arduino board is pressed and released.
 * This example works with the Wiring / Arduino program that follows below.
 */


import processing.serial.*;

Serial myPort;  // Create object from Serial class
int val;      // Data received from the serial port

void setup() 
{
  size(200, 200);
  // I know that the first port in the serial list on my mac
  // is always my  FTDI adaptor, so I open Serial.list()[0].
  // On Windows machines, this generally opens COM1.
  // Open whatever port is the one you're using.
  printArray(Serial.list());
  String portName = Serial.list()[1];
  myPort = new Serial(this, portName, 9600);
}

void draw()
{
  if ( myPort.available() > 0) {  // If data is available,
    val = myPort.read();         // read it and store it in val
  }
  background(255);             // Set background to white
  if (val == 0) {              // If the serial value is 0,
    fill(0);                   // set fill to black
  } 
  else {                       // If the serial value is not 0,
    fill(204);                 // set fill to light gray
  }
  rect(50, 50, 100, 100);
}


- Codigo Arduino:

/*

// Wiring / Arduino Code
// Code for sensing a switch status and writing the value to the serial port.

int switchPin = 4;                       // Switch connected to pin 4

void setup() {
  pinMode(switchPin, INPUT);             // Set pin 0 as an input
  Serial.begin(9600);                    // Start serial communication at 9600 bps
}

void loop() {
  if (digitalRead(switchPin) == HIGH) {  // If switch is ON,
    Serial.write(1);               // send 1 to Processing
  } else {                               // If the switch is not ON,
    Serial.write(0);               // send 0 to Processing
  }
  delay(100);                            // Wait 100 milliseconds

  Codigo Processing (Ejemplo N°2): 

  En este caso usamos un codigo nuevo donde instalamos The MidiBus. MIDI es una interfaz digital de instrumentos musicales, donde este protocolo lo que hace es comunicarse cp dispositivos musicales como; teclados, parlantes, sintetizadores, computadores, etc. Igualmente como  vimos hay guitarras que tienen MIDI. Ademas nosotros podemos hacer la señal de contro o tambien podemos enviarlas nosotros. El cable "MIDI" que se llama DIN se utiliza para enviar mensajes MIDI. MIDI por dentro es serial, para programar este a mano se hace a 115.200. MIDI es un medio para asociar mensajes y enviarlos a un medio que toma esta señal. MIDI es para hacer que muchos instrumentos suenen al mismo tiempo, se pueden procesar varios mensajes en canales distintos. Cuando es MIDI de enviar el numero va en negativo. La notaMIDI % 128 lo que hace es

  // ej_34_midi_enviar
// por montoyamoraga
// para Academia Sinestesia
// Programa de Medios Interactivos 2023
// v0.0.2 mayo 2023
// hecho con Processing 4.2.0
// ejemplo traducido y basado
// de The MidiBus => Basic

// importar biblioteca
import themidibus.*;

// crear instancia de MidiBus
MidiBus bus;

int entradaMIDI = -1;
int salidaMIDI = 2;

int canalMIDI = 0;
int notaMIDI = 0;
int velocidadMIDI = 20;

void setup() {

  size(200, 200);

  frameRate(1);

  // listar todos las midibus
  MidiBus.list();

  bus = new MidiBus(this, entradaMIDI, salidaMIDI);

  textAlign(CENTER, CENTER);
  fill(0);
}

void draw() {

  background(255, 255, 0);
  text("enviar", width/2, height/2);

  // enviar nota MIDI
  bus.sendNoteOn(canalMIDI, notaMIDI, velocidadMIDI);
  
  // actualizar nota MIDI
  notaMIDI = notaMIDI + 1;
  
  notaMIDI = notaMIDI % 128;
}

