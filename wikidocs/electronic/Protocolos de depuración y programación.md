Una **interfaz de programación** es un conjunto de mecanismos que permiten la comunicación entre un programador o depurador externo y el microcontrolador o sistema embebido. A través de esta interfaz, el programador puede enviar instrucciones, cargar código (firmware), realizar pruebas, y depurar el comportamiento del sistema. Estas interfaces son esenciales para el desarrollo y mantenimiento de dispositivos electrónicos.

Las interfaces de programación permiten:

- **Cargar firmware** en la memoria del microcontrolador.
- **Depurar el código** mediante la ejecución paso a paso, análisis de registros internos y observación del flujo de datos.
- **Probar y verificar** que el hardware y el software funcionen correctamente.

# Protocolos de programación
### **SWD (Serial Wire Debug)**

![[swd_connection_method.png]]

El **SWD** es un protocolo de depuración desarrollado por ARM para sustituir a **JTAG** en dispositivos basados en la arquitectura ARM Cortex. Es más simple y utiliza menos pines que JTAG, lo que lo hace más eficiente para sistemas con limitaciones de espacio y pines.

#### Características de SWD:

- **Pines usados**: SWD utiliza **dos pines** principales:
    - **SWDIO** (Serial Wire Debug Input/Output): Línea de datos bidireccional.
    - **SWCLK** (Serial Wire Clock): Línea de reloj. Además, puede requerir un pin adicional para **reset** (opcional) y alimentación.

- **Familias soportadas**:
    - Microcontroladores **ARM Cortex-M** (Cortex-M0, M3, M4, M7) y otros basados en la arquitectura ARM.
- **Velocidad**: Menor cantidad de pines permite un diseño más sencillo, aunque la velocidad de depuración puede ser un poco inferior a JTAG en sistemas más complejos.

### **JTAG (Joint Test Action Group)**

![[jtag_connection_method.png]]

**JTAG** es un protocolo estándar de depuración y prueba que se utiliza para la programación y verificación de circuitos electrónicos y microcontroladores. Fue desarrollado por el consorcio **IEEE 1149.1**.

#### Características de JTAG:

- **Pines usados**: JTAG suele requerir **cuatro o cinco pines**:
    - **TDI** (Test Data In): Entrada de datos.
    - **TDO** (Test Data Out): Salida de datos.
    - **TCK** (Test Clock): Señal de reloj.
    - **TMS** (Test Mode Select): Selección del modo de prueba.
    - **TRST** (Test Reset, opcional): Señal opcional para reiniciar la interfaz.
- **Familias soportadas**:
    - JTAG se utiliza en una amplia gama de microcontroladores, incluyendo familias **ARM**, **MIPS**, **PIC**, **AVR**, y otros dispositivos FPGA y ASIC.
- **Velocidad y capacidad**: JTAG permite pruebas y depuración de múltiples dispositivos en cadena (daisy-chaining), lo que es útil en sistemas con múltiples chips en la misma placa. Es más completo que SWD, pero requiere más pines.