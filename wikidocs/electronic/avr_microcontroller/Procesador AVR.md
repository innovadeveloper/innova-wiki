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

Sustituyendo el valor de 103:

Frecuencia_baudios=16 000 00016×(103+1)=9600Frecuencia\_baudios = \frac{16 \, 000 \, 000}{16 \times (103 + 1)} = 9600Frecuencia_baudios=16×(103+1)16000000​=9600
- Presentación del Black Magic Probe [[wd_BlackMagicProbe Presentación]]
- Servidor GDB y otras implementaciones (OpenCD) [[wd_ServidorGDB]]
