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
# Link del projecto
https://www.tinkercad.com/things/kREDjjAq87N
