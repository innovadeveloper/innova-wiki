#### Que el estándar CMSIS

#### Estructura CMSIS

	![[Screenshot_20240919-073433.jpg]]
	
```shell
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
│   │   └── **system_stm32f1xx.c
│   │
│   └── /Startup
│       └── **startup_stm32f103xb.s
│
├── /Drivers
│   ├── /CMSIS
│   │   ├── /Core
│   │   │   ├── Include
│   │   │   │   ├── *core_cm3.h
│   │   │   │   ├── *cmsis_gcc.h
│   │   │   │   └── *cmsis_compiler.h
│   │   └── /Device
│   │       └── /ST
│   │           └── /STM32F1xx
│   │               └── /Include
│   │                   ├── ***stm32f103xb.h
│   │                   └── ***system_stm32f1xx.h
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
```


#### Explicación de cada tipo de fichero de CMSIS

	CMSIS Core
		CMSIS-Core es el componente principal de CMSIS, que proporciona acceso estandarizado a los núcleos ARM Cortex y define los métodos para interactuar con los registros del núcleo, interrupciones y excepciones. Algunas notas de interés sobre este componente son :
			- ARM proporciona los archivos core_cmX.h porque estos definen cómo interactuar con las características específicas del núcleo ARM Cortex, como el manejo de interrupciones, excepciones, y registros del procesador.
			- Donde "X" representa la versión del núcleo (por ejemplo, core_cm3.h para Cortex-M3 y core_cm4.h para Cortex-M4).
			- ARM proporciona el núcleo de los microcontroladores, es decir, la arquitectura del procesador Cortex-M, pero no define ni controla los periféricos ni la configuración específica del sistema (como los relojes, memorias, etc.) en cada microcontrolador.
		




