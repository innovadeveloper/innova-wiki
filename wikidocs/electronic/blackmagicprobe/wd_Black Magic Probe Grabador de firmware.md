Antes de grabar el firmware del artefacto construido, debemos asegurarnos de haber realizado lo siguiente : 
- Tener el artefacto en formato ".elf"
- Conectar el BMP al ordenador por medio del puerto microusb
- Conectar el STM32 (target) hacia el BMP por medio de la interfaz SWD
![[Pasted image 20240915134532.png|ccms]]

![[Pasted image 20240915133621.png|ccms]]
	
- Ambos STM32 deben estar en modo de flash (Boot0 a 0)

Ahora si a continuar con los siguientes comandos en el shell del sistema.
```shell
# ubicar el primer puerto de comunicación bmp
ls -l /dev/cu.usbmodem*

# conectarse y grabar el firmware
arm-none-eabi-gdb PATH/YOUR_ARTIFACT.elf
(gdb) target extended-remote /dev/cu.usbmodem_YOUR_DIRECTION
	Remote debugging using /dev/cu.usbmodem_YOUR_DIRECTION
(gdb) monitor swdp_scan
	Target voltage: 2.31V
	Available Targets:
	No. Att Driver
	 1      STM32F1 L/M density M3
(gdb) attach 1
	Attaching to program: /Users/kenny/Files/TMP/firmwares/blinkingled.elf, Remote target
	0x1ffff1ec in ?? ()
(gdb) load
	Loading section .isr_vector, size 0x10c lma 0x8000000
	Loading section .text, size 0x10e4 lma 0x800010c
	Loading section .rodata, size 0x24 lma 0x80011f0
	Loading section .init_array, size 0x4 lma 0x8001214
	Loading section .fini_array, size 0x4 lma 0x8001218
	Loading section .data, size 0xc lma 0x800121c
	Start address 0x0800036c, load size 4648
	Transfer rate: 14 KB/sec, 464 bytes/write.
(gdb) monitor reset halt 
	You are now detached from the previous target.
(gdb) continue
	Continuing.
	warning: Remote failure reply: E01
	Could not read registers; remote failure reply 'EFF'
```

Ya finalmente, para comprobar q el firmware se grabò, solo reiniciamos el stm32 target y debería ejecutar si firmware.