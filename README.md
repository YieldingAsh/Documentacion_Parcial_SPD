# Documentacion_Parcial_SPD
![ArduinoTinkercad](https://github.com/YieldingAsh/Documentacion_Parcial_SPD/assets/99512390/bab40be3-f0c3-4d94-9956-880f75f535fe)
# Integrantes
- Matias Nicolas Castrellon
# Visualizacion de proyecto en Tinkercad 
![image](https://github.com/YieldingAsh/Documentacion_Parcial_SPD/assets/99512390/21364ab1-49b4-42f9-a1c9-b82bbe91bf44)
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
-Esta es la funcion principal de loop la cual llama a dos funciones una para mostrar el estado del montacarga que esta detenido y la otra funcion comprueba si quiere subir o bajar.
````
void loop()
{
  led_estado(0);
  subir_bajar(piso);
}
````
-Esta funcion dependiendo del valor recibido en el parametro se encendera un led verde y se apagara el led rojo o se encendera un led rojo y se apagara el led verde.
````
void led_estado(int i)
{
      if (i == 1)
      {
            digitalWrite(ledRojo, LOW);
            digitalWrite(ledVerde, HIGH);
      }
      else
      {
            digitalWrite(ledRojo, HIGH);
            digitalWrite(ledVerde, LOW);
      }
}
````
-Esta funcion con un swich dependiendo del valor recibido en el parametro dirigido para el display de 7 segmentos para la iluminacion de los leds correspondientes para generar la figura de un numero, el numero a generar es el noumero del parametro recibido.
````
void n_led(int piso)
{
 switch(piso)
    {
    case 0:
          digitalWrite(a,HIGH);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,HIGH);
          digitalWrite(e,HIGH);
          digitalWrite(f,HIGH);
          digitalWrite(g,LOW);
  		  break;

    case 1:
          digitalWrite(a,LOW);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,LOW);
          digitalWrite(e,LOW);
          digitalWrite(f,LOW);
          digitalWrite(g,LOW);
          break;
  
    case 2:
          digitalWrite(a,HIGH);
          digitalWrite(b,HIGH);
          digitalWrite(c,LOW);
          digitalWrite(d,HIGH);
          digitalWrite(e,HIGH);
          digitalWrite(f,LOW);
          digitalWrite(g,HIGH);
          break;

    case 3:
          digitalWrite(a,HIGH);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,HIGH);
          digitalWrite(e,LOW);
          digitalWrite(f,LOW);
          digitalWrite(g,HIGH);
          break;

    case 4:
          digitalWrite(a,LOW);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,LOW);
          digitalWrite(e,LOW);
          digitalWrite(f,HIGH);
          digitalWrite(g,HIGH);
          break;

    case 5:
          digitalWrite(a,HIGH);
          digitalWrite(b,LOW);
          digitalWrite(c,HIGH);
          digitalWrite(d,HIGH);
          digitalWrite(e,LOW);
          digitalWrite(f,HIGH);
          digitalWrite(g,HIGH);
          break;

    case 6:
          digitalWrite(a,HIGH);
          digitalWrite(b,LOW);
          digitalWrite(c,HIGH);
          digitalWrite(d,HIGH);
          digitalWrite(e,HIGH);
          digitalWrite(f,HIGH);
          digitalWrite(g,HIGH);
          break;

    case 7:
          digitalWrite(a,HIGH);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,LOW);
          digitalWrite(e,LOW);
          digitalWrite(f,LOW);
          digitalWrite(g,LOW);
          break;

    case 8:
          digitalWrite(a,HIGH);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,HIGH);
          digitalWrite(e,HIGH);
          digitalWrite(f,HIGH);
          digitalWrite(g,HIGH);
          break;

    case 9:
          digitalWrite(a,HIGH);
          digitalWrite(b,HIGH);
          digitalWrite(c,HIGH);
          digitalWrite(d,LOW);
          digitalWrite(e,LOW);
          digitalWrite(f,HIGH);
          digitalWrite(g,HIGH);
          break;
	}
}
````
-Esta funcion es un comporbador el cual matiene el montacarga detenido y llama la funcion de led  para decir que esta parado, se fija si el usuario pulsar el boton deteber, subir o bajar para continuar con la orden anterior impuesta
````
void detener(bool e)
{
      led_estado(0);
      delay(200);
      while (e)
      {
            if (digitalRead(subir) == 1023)
            {
                  e = false;
                  led_estado(1);
                  delay(300);
            }
            else if (digitalRead(bajar) == 1023)
            {
                  e = false;
                  led_estado(1);
                  delay(300);
            }
            else if (digitalRead(parar) == 1)
            {
                  e = false;
                  led_estado(1);
                  delay(300);
            }
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
int piso = 0;
````
-Funcion de setup para declarar los pines tambien para cetear el dispay en cero e inicialicar el serial ademas de imprimer el mensaje del piso en donde se encuentra el monta cargas el cual comienza en 0
````
void setup()
{
      pinMode(a, OUTPUT);
      pinMode(b, OUTPUT);
      pinMode(c, OUTPUT);
      pinMode(d, OUTPUT);
      pinMode(e, OUTPUT);
      pinMode(f, OUTPUT);
      pinMode(g, OUTPUT);
      pinMode(buzzer, OUTPUT);
      pinMode(ledVerde, OUTPUT);
      pinMode(ledRojo, OUTPUT);
      pinMode(ledNaranja, OUTPUT);
      pinMode(parar, INPUT);
      digitalWrite(ledRojo, HIGH);
      Serial.begin(9600);
      n_led(piso);
      Serial.print("Piso : ");
      Serial.print(piso);
}
````
-Esta funcion es la encargada de fijarse si los botones subir y bajar son presionador y empezar a llamar a la funcion para que mueva el montacargas.
````
void subir_bajar(int &piso)
{
      if (digitalRead(subir) == 1023)
      {
            while (piso < 9)
            {
                  piso++;
                  mover(piso);
            }
      }
      else if (digitalRead(bajar) == 1023)
      {
            while (piso > 0)
            {
                  piso--;
                  mover(piso);
            }
      }
      else if (analogRead(alarma) == 1023)
      {
        funcion(true);
      }
}

````
-Esta funcion es la encargada de simular el trayecto de subida y bajada del montacargas ademas de comprobar en el trayecto de los 3 segundos si el boton detener es pulsado en caso de ser asi llama a la funcion para detener el montacargas, continuando con el codigo despues llama a la funcion para imprimi en la consola en que piso se encuentra el montacargas y llamar a la funcion para mostrar en el display de 7 segmentos el numero del piso en el que se encuentra.
````
void mover(int piso)
{
      led_estado(1);
      for (int i = 0; i < 3000; i++)
      {
            if (digitalRead(parar) == 1)
            {
                  detener(true);
            }
            delay(1);
      }
      serial(piso);
      n_led(piso);
      delay(300);
}
````
-Funcion para escribir en que piso esta el montacargas
````
void serial(int piso)
{
      Serial.print("\n");
      Serial.print("Piso : ");
      Serial.print(piso);
}
````
-Funcion envia a la consola una alerta de incedios. enciende un led naranja y hace sonar un piezo por 3 segundos despues lo apaga por un 1 segundo vuelve arrepetirse a menos que se toque de vuelta el boton de incendios
````
void funcion(bool e)
{
  while(e)
  {
     Serial.print("\n");
     Serial.print("Alarma de incendio activada");
     digitalWrite(ledNaranja, HIGH);
     tone(buzzer, 0.1);
     delay(10);
     for (int i = 0; i < 3000; i++)
      {
            if (analogRead(alarma) == 1023)
            {
                  e=false;
            }
            delay(1);
      }
     noTone(buzzer);
     digitalWrite(ledNaranja, LOW);
     delay(1000);
  }
}
````
# Link del projecto
https://www.tinkercad.com/things/kREDjjAq87N
# Link del codigo fuente
https://onlinegdb.com/9e9_7GfI6
