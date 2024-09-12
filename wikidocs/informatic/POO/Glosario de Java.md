## **SOLID**
**SOLID** es un acrónimo que representa cinco principios de diseño que ayudan a crear sistemas de software más robustos, flexibles y mantenibles

**Single reponsability :** Una clase debe tener una única responsabilidad dentro del sistema.
	![[Pasted image 20240912103250.png|200*100]]
**Open / Closed :** El comportamiento de una clase debe poder extenderse sin modificar su código fuente
![[Pasted image 20240912113433.png|400]]
**Liskov Substitution Principle :** Establece que una clase derivada puede reemplazar a su clase base sin afectar el comportamiento del programa.
	![[Pasted image 20240912113510.png | 500]]
**Segregación de la Interfaz :** Establece que una clase no debería ser obligada a implementar interfaces que no necesita.
![[Pasted image 20240912113535.png|600]]
**Inversión de Dependencia :** Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones.
	![[Pasted image 20240912113607.png|600]]
## **Stream**

Un Stream **es una secuencia de elementos que soporta diferentes tipos de operaciones**, como filtrado, mapeo y reducción, aplicándolas de forma fluida. A diferencia de las colecciones, un Stream no almacena datos, sino que trabaja sobre ellos de manera **lazily (perezosa)**, procesando los elementos solo cuando es necesario
![[Pasted image 20240912114444.png|200]]

## **Java Versions**

|Característica|Java 8|Java 9|Java 11|
|---|---|---|---|
|**Lanzamiento**|Marzo 2014|Septiembre 2017|Septiembre 2018|
|**Soporte**|Largo plazo|Soporte estándar|Soporte largo plazo|
|**Lambdas**|Introducción de expresiones lambda|No hay cambios significativos|No hay cambios significativos|
|**Streams API**|Introducción de Streams API|No hay cambios significativos|No hay cambios significativos|
|**API de Fecha y Hora**|Nueva API de Fecha y Hora|No hay cambios significativos|No hay cambios significativos|
|**Módulos**|No soportado|Introducción del sistema de módulos (Project Jigsaw)|Mejoras en el sistema de módulos|
|**JShell**|No disponible|Introducción de JShell (Shell interactivo)|No hay cambios significativos|
|**Modularización del JDK**|No disponible|Introducción del JDK modular|No hay cambios significativos|
|**Métodos Privados en Interfaces**|No disponible|No disponible|Introducción de métodos privados en interfaces|
|**Recolección de Basura**|Implementación de G1 GC|Mejoras en G1 GC y otros GC|Mejoras en G1 GC y otros GC|
|**API de HTTP/2**|No disponible|Introducción de la API HTTP/2|Mejoras en la API HTTP/2|
|**Nuevas Características de la Lengua**|Nuevas características como `Optional`, `Functional Interface`, etc.|No hay cambios significativos|Mejoras en las características del lenguaje|
|**Eliminación de `Java EE`**|No aplicable|No aplicable|Eliminación de módulos `Java EE` y `CORBA`|
|**Herramientas de Compilación**|Introducción de `javac` con nuevas opciones de análisis|Mejoras en el sistema de compilación|Mejoras en el sistema de compilación|

