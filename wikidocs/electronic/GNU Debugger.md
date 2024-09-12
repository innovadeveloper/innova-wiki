**Black Magic Debug**

**Black Magic Debug** es el firmware que implementa el servidor **GNU DeBugger (GDB)** en el hardware **Black Magic Probe**. Su propósito es ofrecer un depurador eficiente para sistemas embebidos, eliminando la necesidad de software intermedio, como **OpenOCD**

![[gnu_debugger_logo.png]]
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

**Componentes requeridos para el flasheo del BMD**

#####  **Software**
- **OpenOCD** es una herramienta que permite flashear y depurar microcontroladores, y contiene muchos archivos de configuración para diferentes interfaces de depuración (como **ST-Link**) y diferentes tipos de microcontroladores (como **STM32F1**)
- **Toolchain ARM GCC**, la librería de gcc :
	- Descarga el archivo **tarball** (normalmente un archivo `.tar.bz2` o `.tar.xz`).
	- https://developer.arm.com/downloads/-/gnu-rm 
	- tar -xvf gcc-arm.tar.bz2
	- agregar la ruta del compilador al PATH del sistema
	- comprobar la versiòn del compilador : **arm-none-eabi-gcc --version**
#####  **Hardware**
- **ST-Link V2** 
- **STM32F103C8T6** **(blue pill)**

### **Construcción del black-magic.bin**
Ejecutar los siguientes comandos :
```shell
# clonación recursiva del repositorio
git clone --recursive https://github.com/blacksphere/blackmagic.git

cd blackmagic

# Para la **Blue Pill**, puedes especificar el **PROBE_HOST** como `stlink` y el **BLUEPILL=1** para compilar el firmware correcto.
make PROBE_HOST=stlink BLUEPILL=1

tree | grep bin

```