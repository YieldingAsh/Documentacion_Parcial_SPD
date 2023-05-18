# Documentacion_Parcial_SPD
![ArduinoTinkercad](https://github.com/YieldingAsh/Documentacion_Parcial_SPD/assets/99512390/bab40be3-f0c3-4d94-9956-880f75f535fe)
# Integrantes
- Matias Nicolas Castrellon
# Visualizacion de proyecto en SPD
![Captura](https://github.com/YieldingAsh/Documentacion_Parcial_SPD/assets/99512390/264504f6-dad7-414a-8db2-90c0e0018c03)
Requisitos del Proyecto:
1) Interfaz de usuario:
• Deberá haber 3 botones, uno para subir pisos, otro para bajar pisos y otro para
detener el montacarga.
• Deberá tener 2 LEDs, uno verde que indicará cuando el montacarga este en
movimiento, otro rojo que indique cuando el montacarga esté pausado.
• En el display 7 segmentos deberán informar en tiempo real en qué piso se
encuentra el elevador.
• Se sabe que el tiempo de trayecto entre pisos es de 3 segundos (3000 ms).
• Se deberá informar por monitor serial el piso en el que se encuentra el
montacarga, este en funcionamiento o en pausa.

2) Funcionamiento del montacarga:
• Implementa un algoritmo que permita que el elevador suba y baje o frene
presionando los botones correspondientes.
• Deberán buscar una forma para pausar el montacargas cuando el usuario lo
determine.
3) Documentación:
• Deberán presentar un diagrama esquemático del circuito y explicar el
funcionamiento aplicado de cada componente.
• Presentar el codigo fuente del proyecto de Arduino listo para ser
implementado.
• Deberán explicar el funcionamiento integral utilizando documentación
MarkDown.
# Funcion principal
-Esta es la funcion principal la cual verifica si se toco el boton de subir o de bajar, ademas de encender el led rojo el cual se enciende cuando esta parado.
````
void loop()
{
  digitalWrite(ledRojo,HIGH);
  arriba = digitalRead(subir);
  if (arriba == true){
  	subiendo();
  };
  abajo = digitalRead(bajar);
  if (abajo == true){
    bajando();
  };
}
````
-Estas Funciones son para el display de 7 segmentos para la iluminacion de los leds correspondientes para generar la figura de un numero, el numero a generar de cada funcion es el nombre mismo de esa funcion.
````
void cero()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,HIGH);
  digitalWrite(e,HIGH);
  digitalWrite(f,HIGH);
  digitalWrite(g,LOW);
}

void uno()
{
  digitalWrite(a,LOW);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,LOW);
  digitalWrite(e,LOW);
  digitalWrite(f,LOW);
  digitalWrite(g,LOW);
}

void dos()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,HIGH);
  digitalWrite(c,LOW);
  digitalWrite(d,HIGH);
  digitalWrite(e,HIGH);
  digitalWrite(f,LOW);
  digitalWrite(g,HIGH);
}

void tres()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,HIGH);
  digitalWrite(e,LOW);
  digitalWrite(f,LOW);
  digitalWrite(g,HIGH);
}

void cuatro()
{
  digitalWrite(a,LOW);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,LOW);
  digitalWrite(e,LOW);
  digitalWrite(f,HIGH);
  digitalWrite(g,HIGH);
}

void cinco()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,LOW);
  digitalWrite(c,HIGH);
  digitalWrite(d,HIGH);
  digitalWrite(e,LOW);
  digitalWrite(f,HIGH);
  digitalWrite(g,HIGH);
}

void seis()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,LOW);
  digitalWrite(c,HIGH);
  digitalWrite(d,HIGH);
  digitalWrite(e,HIGH);
  digitalWrite(f,HIGH);
  digitalWrite(g,HIGH);
}

void siete()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,LOW);
  digitalWrite(e,LOW);
  digitalWrite(f,LOW);
  digitalWrite(g,LOW);
}

void ocho()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,HIGH);
  digitalWrite(e,HIGH);
  digitalWrite(f,HIGH);
  digitalWrite(g,HIGH);
}

void nueve()
{
  digitalWrite(a,HIGH);
  digitalWrite(b,HIGH);
  digitalWrite(c,HIGH);
  digitalWrite(d,LOW);
  digitalWrite(e,LOW);
  digitalWrite(f,HIGH);
  digitalWrite(g,HIGH);
}
````
-Esta funcion es un comporbador el cual se fija si el usuario esta pulsando el boton detener parar asi detener el monta carga
````
void comDetener()
{
  if (detener == true){
    	digitalWrite(ledRojo,HIGH);
    	digitalWrite(ledVerde,LOW);
    	arriba = false;
    	abajo = false;
  	}
}
````
-Estos son todas las variables declaradas
````
int a = 2;
int b = 3;
int c = 4;
int d = 5;
int e = 6;
int f = 7;
int g = 8;
int ledVerde = 9;
int ledRojo = 10;
int bajar = 11;
int parar = 12;
int subir = 13;
int tiempo = 3000;
int arriba = false;
int abajo = false;
int detener = false;
int piso = 0;
````
-Funcion de setup para declarar los pines tambien para cetear el dispay en cero e inicialicar el serial ademas de imprimer el mensaje del piso en donde se encuentra el monta cargas
````
void setup()
{
  pinMode(a,OUTPUT);
  pinMode(b,OUTPUT);
  pinMode(c,OUTPUT);
  pinMode(d,OUTPUT);
  pinMode(e,OUTPUT);
  pinMode(f,OUTPUT);
  pinMode(g,OUTPUT);
  pinMode(ledVerde, OUTPUT);
  pinMode(ledRojo, OUTPUT);
  pinMode(bajar, INPUT);
  pinMode(parar, INPUT);
  pinMode(subir, INPUT);
  cero();
  Serial.begin(9600);
  Serial.print("Piso : ");
  Serial.print(piso);
}
````
-Estas dos funciones son las encargadas de subir y bajar el montacargas e llamar la funcion del numero correspondiente a mostrar en el display
````
void subiendo()
{
  digitalWrite(ledRojo,LOW);
  digitalWrite(ledVerde,HIGH);
  if (arriba == true){
    if (piso == 0)
    {
    piso = 1;
    serial();
  	uno();
  	delay(tiempo);
    detener = digitalRead(parar);
  	comDetener();
    }
  }
  if (arriba == true){
    if (piso == 1)
    {
    piso = 2;
    serial();
  	dos();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 2)
    {
    piso = 3;
    serial();
  	tres();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 3)
    {
    piso = 4;
    serial();
  	cuatro();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 4)
    {
    piso = 5;
    serial();
  	cinco();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 5)
    {
    piso = 6;
    serial();
  	seis();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 6)
    {
    piso = 7;
    serial();
  	siete();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 7)
    {
    piso = 8;
    serial();
  	ocho();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (arriba == true){
    if (piso == 8)
    {
    piso = 9;
    serial();
  	nueve();
  	delay(tiempo);
    detener = true;
    comDetener();
    }
  }
  else{
    detener = true;
    comDetener();
  }
}

void bajando()
{
  digitalWrite(ledRojo,LOW);
  digitalWrite(ledVerde,HIGH);
  if (abajo == true){
    if (piso == 9)
    {
    piso = 8;
    serial();
  	ocho();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 8)
    {
    piso = 7;
    serial();
  	siete();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 7)
    {
    piso = 6;
    serial();
  	seis();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 6)
    {
    piso = 5;
    serial();
  	cinco();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 5)
    {
    piso = 4;
    serial();
  	cuatro();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 4)
    {
    piso = 3;
    serial();
  	tres();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 3)
    {
    piso = 2;
    serial();
  	dos();
  	delay(tiempo);
    detener = digitalRead(parar);
    comDetener();
    }
  }
  if (abajo == true){
    if (piso == 2)
    {
    piso = 1;
    serial();
  	uno();
  	delay(tiempo);
    detener = digitalRead(parar);
  	comDetener();
    }
  }
  if (abajo == true){
    if (piso == 1)
    {
    piso = 0;
    serial();
  	cero();
  	delay(tiempo);
    detener = true;
  	comDetener();
    }
  }
  else{
    detener = true;
  	comDetener();
  }
}
````
-Funcion para escribir en que piso esta el montacargas
````
void serial()
{
  Serial.print("\n");
  Serial.print("Piso : ");
  Serial.print(piso);
}
````
# Link del projecto
https://www.tinkercad.com/things/kREDjjAq87N
# Link del codigo fuente
https://onlinegdb.com/Glc_nr0Af
