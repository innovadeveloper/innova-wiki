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
		
#### Estructura del proyecto generado 

/Proyecto
│
├── /Core
│   ├── /Inc
│   │   ├── main.h
│   │   ├── stm32f1xx_it.h
│   │   ├── stm32f1xx_hal_conf.h
│   │   └── syscalls.h
│   │
│   ├── /Src
│   │   ├── main.c
│   │   ├── stm32f1xx_hal_msp.c
│   │   ├── stm32f1xx_it.c
│   │   ├── syscalls.c
│   │   └── system_stm32f1xx.c
│   │
│   └── /Startup
│       └── startup_stm32f103xb.s
│
├── /Drivers
│   ├── /CMSIS
│   │   ├── /Core
│   │   │   ├── Include
│   │   │   │   ├── core_cm3.h
│   │   │   │   ├── cmsis_gcc.h
│   │   │   │   └── cmsis_compiler.h
│   │   └── /Device
│   │       └── /ST
│   │           └── /STM32F1xx
│   │               └── /Include
│   │                   ├── stm32f103xb.h
│   │                   └── system_stm32f1xx.h
│   │
│   └── /STM32F1xx_HAL_Driver
│       ├── /Inc
│       │   └── stm32f1xx_hal.h
│       └── /Src
│           └── stm32f1xx_hal.c
│
├── /STM32CubeIDE
│   ├── .project
│   ├── .cproject
│   └── STM32F103C8T6.ioc
│
└── Makefile



Descripción de la Estructura Generada

1. Directorio /Core

Este directorio contiene el código central del proyecto. Incluye el archivo main.c, donde resides el código principal de tu aplicación, junto con otros archivos esenciales de configuración y de interrupciones.

/Core/Inc: Aquí se encuentran los archivos de cabecera (.h) principales.

main.h: Archivo de cabecera para el archivo main.c, donde puedes definir variables globales y funciones.

stm32f1xx_it.h: Este archivo contiene las declaraciones de las funciones de manejo de interrupciones (Interrupt Handlers).

stm32f1xx_hal_conf.h: Archivo de configuración del HAL (Hardware Abstraction Layer), donde puedes habilitar o deshabilitar funcionalidades del HAL.

syscalls.h: Declaraciones para las funciones de llamadas al sistema (system calls).


/Core/Src: Contiene los archivos fuente (.c).

main.c: Este es el archivo principal donde escribirás el código de tu aplicación.

stm32f1xx_hal_msp.c: Contiene las funciones de soporte específico del microcontrolador (MSP) necesarias para el HAL.

stm32f1xx_it.c: Implementa los manejadores de interrupciones del microcontrolador.

system_stm32f1xx.c: Código para la inicialización del sistema (configuración del reloj, etc.).


/Core/Startup: Contiene el archivo de arranque (startup file) escrito en ensamblador.

startup_stm32f103xb.s: Es el archivo de inicio que configura la tabla de vectores y maneja el arranque del microcontrolador. Este archivo es crítico porque define los puntos de entrada del programa y las interrupciones.



2. Directorio /Drivers

Este directorio contiene los drivers o controladores necesarios para interactuar con el hardware del microcontrolador STM32 y los archivos CMSIS que son estándar para el desarrollo en microcontroladores ARM Cortex.

/CMSIS: Contiene los archivos CMSIS (Cortex Microcontroller Software Interface Standard) que proporcionan acceso al núcleo ARM Cortex y a las funciones específicas del dispositivo.

/CMSIS/Core/Include: Contiene los archivos CMSIS-Core necesarios para interactuar con el núcleo ARM Cortex-M.

core_cm3.h: Archivo de cabecera que define el acceso a los registros del núcleo y las funciones del procesador Cortex-M3.

cmsis_gcc.h: Archivo con las definiciones específicas para el compilador GCC.

cmsis_compiler.h: Definiciones generales de CMSIS para la compatibilidad con diferentes compiladores.


/CMSIS/Device/ST/STM32F1xx/Include: Contiene los archivos específicos del dispositivo STM32F103C8T6.

stm32f103xb.h: Archivo de cabecera con las definiciones de los registros y periféricos específicos del STM32F103.

system_stm32f1xx.h: Define la inicialización del sistema, como la configuración del reloj y otras funciones del sistema.



/STM32F1xx_HAL_Driver: Este directorio contiene los archivos del Hardware Abstraction Layer (HAL), que proporcionan una capa de abstracción para interactuar con los periféricos del microcontrolador sin tener que escribir código de bajo nivel para manejar los registros directamente.

/Inc: Contiene los archivos de cabecera del HAL, como stm32f1xx_hal.h.

/Src: Contiene los archivos fuente del HAL, donde están implementadas las funciones para interactuar con los periféricos del microcontrolador.



3. Directorio /STM32CubeIDE

Este directorio contiene archivos específicos del entorno STM32CubeIDE.

.project y .cproject: Archivos de configuración del proyecto y del compilador que definen cómo se estructura y compila el proyecto dentro de STM32CubeIDE.

STM32F103C8T6.ioc: Este es el archivo de configuración de STM32CubeMX, que guarda la configuración de pines y periféricos que has realizado en la herramienta de CubeMX. Si lo abres en STM32CubeMX, puedes modificar la configuración del microcontrolador y regenerar el código.


4. Otros Archivos

Makefile: Este archivo es generado si seleccionaste GNU Make como tu toolchain. Define las reglas para compilar el proyecto usando el compilador GCC ARM. Este archivo permite compilar el proyecto desde la línea de comandos o integrarlo en otros entornos de desarrollo fuera de STM32CubeIDE.



---

Resumen de la Estructura

/Core: Contiene el código principal de tu aplicación, las interrupciones y el archivo de inicio (startup).

/Drivers: Incluye los archivos CMSIS y los controladores HAL necesarios para interactuar con el hardware del STM32F103.

/STM32CubeIDE: Contiene archivos de configuración específicos del IDE.

Makefile: Para la compilación del proyecto usando GNU Make.

Configuración del nuevo proyecto en platformio