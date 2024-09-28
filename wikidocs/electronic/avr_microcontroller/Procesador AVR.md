En este **wikidoc** se presenta el siguiente alcance con el objetivo de mostrar como poder utilizar un ATMega328P como microcontrolador de desarrollo, usando la interface ISP y el grabador USBasp.
	![[Pasted image 20240927120434.png]]
**Alcances**
- Configuración del reloj y su divisor de frecuencia para trabajar con UART
	- Para calcular el divisor de frecuencia UBRR (Registro Baud Rate USART)
	- 
		$$
		UBRR = \frac{F_{osc}}{16 \times Baud} - 1
		$$
		**Donde**:
		- **Fosc**​ es la frecuencia de oscilación o frecuencia del reloj del microcontrolador (16 MHz).
		- **Baud** es la velocidad de baudios que deseas configurar (9600 baudios en este caso).
		- **16**: Es el factor de oversampling, debido a los 16 muestreos por bit.
		$$
		UBRR = \frac{16 \, 000 \, 000}{16 \times 9600} - 1
		$$
		$$
		UBRR = \frac{16 \, 000 \, 000}{153600} - 1
		$$
		$$ 
		UBRR \approx 103.1667 - 1
		$$
		$$ 
		UBRR \approx 102.1667
		$$

	- El microcontrolador tiene un reloj principal que corre a 16 MHz, lo que es demasiado rápido para la mayoría de las comunicaciones UART.
	- Para lograr una velocidad de 9600 bits por segundo (baudios), debes reducir la velocidad de la señal serial.
$$
	Frecuencia\_baudios = \frac{F_{osc}}{16 \times (UBRR + 1)}
$$
			$$
				Frecuencia_baudios=16×(103+1)16000000​=9600​​
		$$
- Configuración del reloj externo
	- Se requiere tener instalado : avrdude
	- Que son los fusibles y cuales son sus tipos
	- Riesgos de cambiar a un oscilador externo
		- Si configuras mal los fuse bits relacionados con la fuente de reloj, el microcontrolador podría esperar una señal de reloj externa que no existe, lo que lo bloquearía. Para desbloquearlo se necesitaría un programador avr de alto voltaje para reprogramarlo y volverlo a su reloj interno o externo. En caso de que ocurra puede evaluarse las siguientes opciones : 
			- Utilizar un oscilador externo temporal de la frecuencia q requiera el microcontrolador
			- Reconfigurar nuevamente con el usbasp por si se tuviera suerte :
				- ``` avrdude -c usbasp -p m328p -U lfuse:w:0x62:m ```
				- ``` [0x62] Este comando establecería los fuse bits para usar un reloj interno de 8 MHz (ajustable por software), que podría ser suficiente para volver a recuperar el control ```
	- Comando para leer los fuse bits del microcontrolador:
		- ``` avrdude -c usbtiny -p m328p -U lfuse:r:-:h ```
	- Comando para setear el tipo de oscilador
		- ```shell avrdude -c usbasp -p m328p -U lfuse:w:0xFF:m ```
		- ``` [-c] tipo de programador, [-p] modelo del microcontrolador, [-U] indica q realizaremos una operación de escritura en un espacio de memoria específico del microcontrolador, [lfuse] se refiere a los lowfuse, [:w] indica q estamos escribiendo un valor, [:0xFF] el valor q escribiremos en formato hexadecimal, [:m] significa q estamos trabajando en el modo fuse```
	- Explicación de la tabla (Low Fuse)
		- Tabla de Registro de Low Fuse Bits ![[Pasted image 20240928142149.png|clms]]
		- Configuración de low fuse bits para un oscilador de cristal de 16 Mhz (externo) ![[Pasted image 20240928142434.png|clms]]
		- Configuración de low fuse bits para un oscilador de cristal de 8 Mhz (interno) ![[Pasted image 20240928142813.png|clbs]]
		- Tabla CKSEL para diferentes fuentes de reloj ![[Pasted image 20240928142923.png|clbs]]
	  
- Inserción de código para configurar el UBRR : 
	```c
unsigned int ubrr = 103;  // UBRR para 9600 baudios y 16 MHz
UBRR0H = (unsigned char)(ubrr >> 8);
UBRR0L = (unsigned char)ubrr;
UCSR0B = (1 << RXEN0) | (1 << TXEN0);  // Habilitar receptor y transmisor
UCSR0C = (1 << UCSZ01) | (1 << UCSZ00);  // Configurar 8 bits de datos
```
