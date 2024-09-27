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

- Inserción de código para configurar el UBRR : 
	```c
unsigned int ubrr = 103;  // UBRR para 9600 baudios y 16 MHz
UBRR0H = (unsigned char)(ubrr >> 8);
UBRR0L = (unsigned char)ubrr;
UCSR0B = (1 << RXEN0) | (1 << TXEN0);  // Habilitar receptor y transmisor
UCSR0C = (1 << UCSZ01) | (1 << UCSZ00);  // Configurar 8 bits de datos
```
