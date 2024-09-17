Configuración gráfica del microcontrolador
![[Pasted image 20240916061914.png]]
![[Pasted image 20240916062006.png]]
![[Pasted image 20240916062213.png]]
![[Pasted image 20240916063312.png]]
![[Pasted image 20240916063347.png]]
	La configuración del reloj se hace de izquierda a derecha. Empezamos con el PLL a HSE, luego el PLL Mul., luego el System Clock Mux a PLLCLK, y finalmente ajustamos la preescala a 2 para q PLCK1 quite su error.

![[Pasted image 20240916063604.png]]
![[Pasted image 20240916063644.png|400]]
![[Pasted image 20240916063707.png|400]]
![[Pasted image 20240916063758.png]]
![[Pasted image 20240916065001.png]]
```md
/project_name
    /include          <-- Aquí copias Core/Inc
    /src              <-- Aquí copias Core/Src y Core/Startup
    /lib
        /CMSIS        <-- Aquí copias Drivers/CMSIS
        /STM32F1xx_HAL_Driver  <-- Aquí copias Drivers/STM32F1xx_HAL_Driver
    platformio.ini


```

	![[Pasted image 20240916065020.png|400]]
	![[Pasted image 20240916220359.png|400]]
		

Configuración del nuevo proyecto en platformio