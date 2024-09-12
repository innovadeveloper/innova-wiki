Más información : 
- https://hackaday.io/project/187043/instructions
- https://www.printables.com/es/model/172889-stm32-blue-pill-case-blackmagic-programmer
	- Información y descarga del binario para stm32 : 
		- ![[Pasted image 20240912161835.png|300]]
- https://github.com/blackmagic-debug/blackmagic/blob/main/src/platforms/stlink/platform.h
	- ahì contiene todas las variables del pinout para stlink/stm32 : 
		- **SWDIO**: Puerto **GPIOB**, Pin **14** (PB14)
		- **SWCLK**: Puerto **GPIOA**, Pin **5** (PA5)
### Grabado de firmware en stm32

¡Sí! Puedes utilizar el ST-Link Utility o el STM32CubeProgrammer (anteriormente conocido como ST-Link Programmer) para flashear el firmware de Black Magic Debug en tu Blue Pill en lugar de usar OpenOCD. Ambas herramientas son proporcionadas por STMicroelectronics y son totalmente compatibles con los programadores ST-Link.

Pasos para flashear el firmware usando STM32CubeProgrammer (recomendado):

1. Descargar STM32CubeProgrammer:

Puedes descargar STM32CubeProgrammer desde el sitio oficial de STMicroelectronics: STM32CubeProgrammer.

Esta herramienta reemplaza a ST-Link Utility y es la recomendada por STMicroelectronics.



2. Instalar STM32CubeProgrammer:

Sigue las instrucciones de instalación para tu sistema operativo (Windows, macOS, Linux).



3. Conectar el ST-Link y la Blue Pill:

Conecta los pines SWDIO, SWCLK, GND, y VCC de tu ST-Link a los correspondientes pines de la Blue Pill.

![[Pasted image 20240912143642.png|300]]
![[Pasted image 20240912164602.png|400]]

Activar el modo de bootloader para grabar código con el jumper **boot-0** en 1
![[Pasted image 20240912144830.png|300]]

![[Pasted image 20240912144941.png|400]]
Conecta el ST-Link a tu computadora mediante el cable USB.



4. Abrir STM32CubeProgrammer:

Inicia STM32CubeProgrammer y selecciona la opción para conectarte a través de ST-Link.

El programa detectará el microcontrolador STM32F103C8T6 de la Blue Pill.



5. Cargar el archivo binario:

En el menú principal, selecciona "Open File" y navega hasta el archivo **blackmagic.bin** que generaste en la compilación. Este archivo debería estar en el directorio src/ del repositorio que compilaste.



6. Seleccionar dirección de memoria:

Asegúrate de que la dirección de escritura sea 0x08000000, que es el comienzo de la memoria flash en la Blue Pill.



7. Flashear el firmware:

Haz clic en el botón "Start Programming" para cargar el firmware en la Blue Pill.

El proceso debería tomar unos segundos, y al finalizar te mostrará un mensaje de éxito si todo ha ido bien.




Usando ST-Link Utility (Windows):

Si prefieres usar ST-Link Utility en lugar de STM32CubeProgrammer (solo disponible en Windows), los pasos son muy similares:

1. Descargar ST-Link Utility:

Puedes descargar ST-Link Utility desde STMicroelectronics.



2. Instalar y conectar:

Instala el software y conecta el ST-Link a tu Blue Pill como lo harías con STM32CubeProgrammer.



3. Abrir ST-Link Utility:

Abre la aplicación y selecciona "Target -> Connect" para detectar la Blue Pill.



4. Flashear el archivo binario:

Selecciona "Target -> Program" y carga el archivo blackmagic.bin.

Asegúrate de que la dirección de inicio sea 0x08000000.

Haz clic en "Start" para flashear el firmware.




Resumen de opciones:

STM32CubeProgrammer es la herramienta más actualizada y recomendada por STMicroelectronics.

ST-Link Utility es una alternativa más antigua pero aún válida, si prefieres usarla.


Ambas herramientas son perfectamente capaces de flashear el firmware de Black Magic Debug en tu Blue Pill y puedes utilizarlas en lugar de OpenOCD si lo prefieres.


![[Pasted image 20240912162001.png|300]]
### **Conexion y Grabado de firmware entre dos dispositivos**

Una vez que hayas instalado el firmware de Black Magic Debug (BMP) en tu STM32 (Blue Pill), puedes utilizarla para programar y depurar otros microcontroladores STM32 a través de SWD (Serial Wire Debug). A continuación te guiaré paso a paso sobre cómo utilizar la Blue Pill con Black Magic Debug para programar otro microcontrolador STM32.

Materiales requeridos:

1. Blue Pill con Black Magic Debug (actuando como el depurador).


2. Otro microcontrolador STM32 que quieras programar.


3. Cables para realizar las conexiones SWD entre ambas placas.


4. GDB (GNU Debugger) en tu computadora para comunicarte con la Blue Pill.
	1. Solo basta tener en el sistema "arm-none-eabi-gdb"
```shell
% which arm-none-eabi-gdb
/usr/local/bin/arm-none-eabi-gdb 		
```
1. Un entorno de programación para generar el archivo de firmware que deseas grabar en el STM32 objetivo (por ejemplo, STM32CubeIDE).



Pasos para grabar código en otro STM32 a través de SWD:

1. Conectar la Blue Pill al STM32 objetivo

Primero, debes realizar las conexiones SWD entre la Blue Pill con BMP y el STM32 que deseas programar.


Conexiones SWD:
![[Pasted image 20240912164108.png|400]]
Blue Pill (BMP) -> STM32 objetivo:

SWDIO (PB14 en Blue Pill) -> SWDIO en el STM32 objetivo.

SWCLK (PA5 en Blue Pill) -> SWCLK en el STM32 objetivo.

GND -> GND.

VCC -> VCC (solo si deseas alimentar el STM32 objetivo desde la Blue Pill).
![[Pasted image 20240912173232.png|400]]

![[Pasted image 20240912173219.png|400]]
Si deseas también controlar el reinicio del STM32 objetivo, puedes conectar el pin RESET de la Blue Pill al pin NRST del STM32 objetivo, aunque no siempre es necesario.



2. Conectar la Blue Pill a tu computadora

Conecta la Blue Pill (ahora con Black Magic Debug) a tu computadora a través de un cable USB. Debería ser detectada como un puerto serie.

```shell
# lista los dispositivos seriales (mac os)
ls /dev/tty.*

```
3. Iniciar GDB en tu computadora

Abre una terminal en tu computadora y ejecuta GDB. Si estás usando STM32CubeIDE, este ya incluye GDB, pero también puedes usar una instalación independiente de GDB.

Si estás en Linux o macOS, el dispositivo podría aparecer como /dev/ttyACM0 o similar. En Windows, aparecerá como un puerto COM (por ejemplo, COM3).

Para iniciar GDB y conectarte a la Blue Pill con Black Magic Debug, usa el siguiente comando:

arm-none-eabi-gdb


4. Conectar GDB al servidor GDB en la Blue Pill

Ahora que GDB está ejecutándose, debes conectarte al servidor GDB que está corriendo dentro de la Blue Pill (BMP). Usa el siguiente comando en la consola de GDB para conectarte:

target extended-remote /dev/ttyACM0

Asegúrate de reemplazar /dev/ttyACM0 con el nombre correcto del puerto donde está conectada tu Blue Pill. En Windows, sería algo como target extended-remote COM3.



5. Detección del microcontrolador STM32 objetivo

Después de conectarte a la Blue Pill, debes detectar el STM32 objetivo. Usa este comando en GDB para buscar el objetivo conectado a través de SWD:

monitor swdp_scan

Esto te mostrará los dispositivos conectados al bus SWD, donde debe aparecer el STM32 que deseas programar.


6. Seleccionar el microcontrolador STM32 objetivo

Después de hacer el escaneo, selecciona el objetivo con este comando en GDB:

attach 1

(Si 1 es el índice del STM32 objetivo que fue detectado en el escaneo anterior. Si no, ajusta el número al índice correcto).


7. Cargar el firmware en el STM32 objetivo

Ahora que estás conectado al STM32 objetivo, puedes cargar un archivo binario .bin o .elf que hayas generado previamente (por ejemplo, en STM32CubeIDE). Usa el siguiente comando para cargar el archivo en la memoria flash del STM32 objetivo:

load path/to/firmware.bin

Este comando grabará el archivo de firmware en la memoria del STM32.


8. Verificar y reiniciar

Una vez que el firmware ha sido grabado con éxito, puedes verificar que todo esté en orden. Si es necesario, puedes reiniciar el STM32 objetivo con el siguiente comando:

monitor reset


9. Ejecutar el programa

Finalmente, puedes ejecutar el programa en el STM32 objetivo utilizando el comando:

continue


Esto permitirá que el STM32 objetivo comience a ejecutar el código que acabas de cargar.

Resumen de los pasos:

1. Conectar la Blue Pill (BMP) a través de SWD a tu STM32 objetivo.


2. Conectar la Blue Pill (BMP) a tu computadora por USB.


3. Iniciar GDB en tu computadora y conectarte a la Blue Pill.


4. Detectar el microcontrolador STM32 objetivo con monitor swdp_scan.


5. Cargar el archivo de firmware en el STM32 objetivo con el comando load.


6. Ejecutar el programa o reiniciar el STM32 objetivo con monitor reset.



Conclusión:

Una vez que hayas configurado la Blue Pill como un Black Magic Probe, puedes usarla para programar y depurar otros microcontroladores STM32 de manera eficiente a través de SWD, todo controlado desde GDB. Este método te permite realizar tanto la programación como la depuración de manera rápida y efectiva sin necesidad de herramientas adicionales como ST-Link o J-Link.





