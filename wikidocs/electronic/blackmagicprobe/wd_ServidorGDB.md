![[Pasted image 20240915120642.png|ccbs]]

#### **¿Qué es un Servidor GDB?**

Un **Servidor GDB (GNU Debugger Server)** es una aplicación que actúa como intermediario entre el depurador GDB y el sistema embebido o la aplicación que se está depurando. Facilita la comunicación remota, permitiendo a los desarrolladores depurar código que se ejecuta en hardware físico, entornos virtuales o sistemas embebidos desde una máquina de desarrollo.

#### **¿Para Qué Sirve?**

El Servidor GDB permite:

- **Depuración Remota:** Conectar GDB a un sistema objetivo que puede estar en una ubicación física diferente o en un entorno virtual.
- **Interacción con Hardware:** Facilitar la depuración de microcontroladores, procesadores y otros dispositivos embebidos mediante interfaces como JTAG o SWD.
- **Control de Ejecución:** Permitir a los desarrolladores iniciar, detener, pausar y controlar la ejecución del programa en el sistema objetivo.
- **Inspección y Modificación de Memoria:** Acceder y modificar el contenido de la memoria del sistema objetivo durante la depuración.

#### **Aplicaciones Comunes**

- **Desarrollo de Firmware:** Depuración de aplicaciones embebidas en microcontroladores como STM32, ARM Cortex-M, entre otros.
- **Desarrollo de Sistemas Operativos:** Depuración de componentes del kernel y otros módulos del sistema operativo.
- **Aplicaciones de Tiempo Real:** Depuración de aplicaciones que requieren tiempos de respuesta precisos y deterministas.
- **Prototipado y Validación de Hardware:** Verificación del funcionamiento correcto del hardware durante el desarrollo.

#### **Ventajas de Utilizar un Servidor GDB**

- **Flexibilidad:** Permite la depuración en una amplia variedad de entornos y plataformas.
- **Eficiencia:** Facilita la identificación y corrección de errores de manera más rápida y precisa.
- **Compatibilidad:** Compatible con múltiples lenguajes de programación y tipos de aplicaciones.
- **Integración con Herramientas de Desarrollo:** Se integra fácilmente con entornos de desarrollo integrados (IDEs) y otras herramientas de desarrollo.
- **Acceso Remoto:** Posibilita la depuración de sistemas que no están físicamente accesibles, mejorando la colaboración y la eficiencia en equipos distribuidos.
### **Tabla de Comandos Comunes de GDB**

![[Pasted image 20240915120924.png|ccbs]]

| **Comando**                | **Descripción**                                                                      |
| -------------------------- | ------------------------------------------------------------------------------------ |
| `break <ubicación>`        | Establece un punto de interrupción en la ubicación especificada (función o línea).   |
| `run`                      | Inicia la ejecución del programa desde el inicio.                                    |
| `continue`                 | Reanuda la ejecución del programa hasta el siguiente punto de interrupción.          |
| `step`                     | Ejecuta la siguiente línea de código, entrando en funciones llamadas.                |
| `next`                     | Ejecuta la siguiente línea de código, sin entrar en funciones llamadas.              |
| `print <expresión>`        | Muestra el valor de la expresión especificada.                                       |
| `list`                     | Muestra el código fuente alrededor de la línea actual.                               |
| `info registers`           | Muestra el estado actual de los registros del procesador.                            |
| `backtrace`                | Muestra la pila de llamadas actual (call stack).                                     |
| `disconnect`               | Desconecta el servidor GDB del objetivo sin cerrar GDB.                              |
| `monitor <comando>`        | Envía un comando específico al servidor GDB (útil para comandos avanzados).          |
| `load`                     | Carga el programa ejecutable en el sistema objetivo.                                 |
| `kill`                     | Finaliza la ejecución del programa en el objetivo.                                   |
| `set <variable> = <valor>` | Asigna un nuevo valor a una variable específica durante la depuración.               |
| `watch <expresión>`        | Establece un punto de observación que pausa la ejecución cuando la expresión cambia. |
| `info breakpoints`         | Muestra la lista de puntos de interrupción establecidos.                             |
| `delete <número>`          | Elimina el punto de interrupción especificado por su número.                         |
