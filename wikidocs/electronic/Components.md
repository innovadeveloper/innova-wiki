**Black Magic Debug**

**Black Magic Debug** es el firmware que implementa el servidor **GNU DeBugger (GDB)** en el hardware **Black Magic Probe**. Su propósito es ofrecer un depurador eficiente para sistemas embebidos, eliminando la necesidad de software intermedio, como **OpenOCD**


**GDB**

Es una aplicación que se ejecuta en el hardware de depuración (como el **BMP**) y permite que el depurador **GDB** de tu computadora se comunique con el microcontrolador. En este caso, el BMP se encarga de ejecutar este servidor GDB en el propio hardware, lo que elimina la necesidad de un software intermedio como **OpenOCD** o **Segger J-Link**.

**Funciones :** 
- **Depuración directa**
- **Comunicaciones estandarizadas**
- **Establecimiento de puntos de interrupción (breakpoints)**
- **Inspección y modificación del estado del microcontrolador**
- **Programación de memoria flash**
- **Puntos de vigilancia (watchpoints)**
- **Compatibilidad con múltiples arquitecturas**
- **Ejecución paso a paso**
- **Sin necesidad de software intermedio**
