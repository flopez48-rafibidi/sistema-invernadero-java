# Análisis y diseño

## 1. Descripción del problema
1.- Se pretende representar un *invernadero inteligente* donde se pretende monitorear algunas condiciones ambientales
para conocer el estado del entorno y hacer una comparacion para tomar acciones cuando sea necesario.

2.- Se va a usar la informacion recibida por sensores para que se encarguen de proporcionar una medicion, obviamente cada sensor
debe depoder identificarse, conocer su ubicacion y el estado en el que se encuentra.

3.- Como el invernadero depende mucho de la humedad podriamos decir que el sistema de riego se encargaria de esos, como tambien 
para la temperatura.

4.- El sistema debera de interpretar las mediciones obtenidas, conocer las condiciones del invernadero y
actuar como nos pida el usuario dependiendo.


## 2. Identificación de objetos

1.- **Sensor de temperatura ambiental**.- Se encarga de obtener la medicion de temperatura dentro del invernadero, este elemento 
independiente es el que proporciona la medicion que va a ser interpretada. Tiene como responsabilidad obtener y representar una medida
e interpretarla segun sea baja, normal o alta.

2.- **Sensor de humedad del suelo**.- Dispositivo encargado de medir la humedad del suelo donde estan las plantas, este sensor 
tiene como funcion si es necesario ativar el riego o no. Su importancia es obtener y representar la humedad del suelo, dependiendo de esa informacion
se tome alguna desicion sobre el riego.

3.- **Aspersores de riego**.- Es el dispositivo que se encarga de regar las plantas y sufuncion podria desirse que es el final, el que depende de todos los sensores
 y permite actuar sobre las plantas. Es el estado de riego con la funcion basica de hechar agua o no de pendiendo de la medicion de los sensores.

## 3. Estado y comportamiento

| Objeto propuesto    | Responsabilidad                                                     | Informacion que debe conservar                                                                                | Comportamientos que debe realizar                                           |
|---------------------|---------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------|
| Sensores            | Solo deben de ser capaces de hacer las mediciones y transmitirlas   | +Identificacion del tipo de sensor <br/> +Lectura de temperatura requerida <br/> +Lectura de humedad obtenida | +Consultar la temperatura o humedad actual <br> +Mandar la lectura obtenida |
| Aspersores de riego | Debe de lograr transmitir el estado en el que se encuentra (on/off) | +Identificacion de cual aspersor es <br/> +Estado de operacion                                                | +Consultar su estado (on/off)                                               |

## 4. Características comunes y especialización

1.- Lo unico que tienen en comun los sensores es el tipo de objeto que son, son sensores.
2.- Ambos tipos de sensores se encargan de obtener una medicion.
3.- Cambian la referencia de medicion que estan haciendo, los de humedad deben de tener una variable diferente al de temperatura ambiental.
4.- Si, todos son clase sensor.
5.- Podriamos decir que uno se especializa en cierto tipo de lugares donde el algun otro no podria obtener nada util.

## 5. Relaciones entre objetos
Un **sensor de temperatura ambiente** es un SENSOR
Un **sensor de humedad del suelo** es un SENSOR
Un **aspersor de riego** es un actuador

Como ambos sensores no estan relacionados por que tienen un tipo diferente de informacion no podrian relacionarse uno con otro directamente. Y
el aspersor no tendria nada que ver con la misma jerarquia ni nada ya que el aspersor de riego solo se encarga de actuar sobre el entorno, tienen
responsabilidades distintas.

El sistema utiliza los sensores para conocer la informacion del entorno.

* La medicion del sensor de humedad del suelo se usa para determinar el riego.
* La medicion del sensor de temperatura para conocer si el estado del ambiente es bajo, adecuado o alto.
* El aspersor de riego solo debe de realizar la accion de regar cuando se requiere.

Podria existir una herencia si hubiera un sensor general con diferentes tipos de sensores.

Las características y comportamientos comunes de los sensores no deberían definirse nuevamente en cada tipo de sensor. Por ejemplo, la identificación, 
el estado y las características generales de un sensor podrían pertenecer al concepto general de sensor, 
mientras que cada sensor específico se encargaría de su propia medición e interpretación.

**SistemaRiego** no debería ser una subclase de Sensor porque no realiza la misma función que un sensor.
Por que el **SistemaRiego** solo utiliza la informacion de los sensores para decidir cuando debe de activarse o desactivarse.