En este wikidoc se indicarán los pasos para los siguientes procesos :
	- Grabado de firmware black_magic.duf.bin por SWD
	- Grabado de firmware black_magic.bin por USB
	- Detección de black_magic_probe

#### **Construcción del firmware black_magic_bin**
```shell
git clone --recursive https://github.com/blackmagic-debug/blackmagic.git
cd blackmagic

# usaremos la compatibilidad stlink
sudo make PROBE_HOST=stlink BLUEPILL=1

# revisamos los binarios construidos dentro del directorio "src"
tree | grep bin

	├── blackmagic.bin
    ├── blackmagic_dfu.bin
```
#### **Grabado de firmware black_magic.dfu.bin por SWD**
Para esto tendremos ya q haber conectado el STLINK al ordenador por medio de su cable USB y su interface SWD hacia el STM32 :
![[Pasted image 20240915124838.png|ccbs]]
Colocamos el STM32 en modo bootloader, esto se consigue colocando el jumper del boot0 a 1.
![[Pasted image 20240912144941.png|ccbs]]
![[Pasted image 20240912144830.png|ccbs]]
Ahora procederemos a abrir el programa STM32CubeProgrammer e instalaremos el "blackmagic_dfu.bin"
![[Pasted image 20240915125647.png|ccbs]]

Para verificar q se grabó correctamente el firmware DFU de BMP realizamos la siguientes acciones : 
- Regresar el **boot0** del stm32 (bmp) a 0 para que cargue la memoria flash.
- Comprobar los dispositivos dfu conectados
```shell
# instalar utilitario dfu en mac
brew install dfu-util

# revisar los dispositivos dfu (opción 1)
dfu-util -l
	dfu-util 0.11
	
	Copyright 2005-2009 Weston Schmidt, Harald Welte and OpenMoko Inc.
	Copyright 2010-2021 Tormod Volden and Stefan Schmidt
	This program is Free Software and has ABSOLUTELY NO WARRANTY
	Please report bugs to http://sourceforge.net/p/dfu-util/tickets/
	
	Found DFU: [1d50:6017] ver=0100, devnum=2, cfg=1, intf=0, path="1-1.1", alt=0, name="@Internal Flash   /0x08000000/8*001Ka,120*001Kg", serial="7EB87A97"

# revistar los dispositivos dfu (opción 2)
system_profiler SPUSBDataType
	USB:
	
	    USB 3.1 Bus:
	
	      Host Controller Driver: AppleT8103USBXHCI
	
	    USB 3.1 Bus:
	
	      Host Controller Driver: AppleT8103USBXHCI
	
	        USB2.0 HUB:
	
	          Product ID: 0x0101
	          Vendor ID: 0x1a40  (TERMINUS TECHNOLOGY INC.)
	          Version: 1.00
	          Speed: Up to 480 Mb/s
	          Location ID: 0x01100000 / 1
	          Current Available (mA): 500
	          Current Required (mA): 100
	          Extra Operating Current (mA): 0
	
	            Black Magic Probe DFU (ST-Link/v2) v1.10.0-1223-g309a17ce:
	
	              Product ID: 0x6017
	              Vendor ID: 0x1d50
	              Version: 1.00
	              Serial Number: 7EB87A97
	              Speed: Up to 12 Mb/s
	              Manufacturer: Black Magic Debug
	              Location ID: 0x01110000 / 2
	              Current Available (mA): 500
	              Current Required (mA): 100
	              Extra Operating Current (mA): 0
```
Importante identificar la dirección de nuestro BMP, en la salida del primer comando "dfu-util -l" pudimos obtener la dirección :
```

Found DFU: [1d50:6017] ver=0100, devnum=2, cfg=1, intf=0, path="1-1.1", alt=0, name="@Internal Flash   /0x08000000/8*001Ka,120*001Kg", serial="7EB87A97"

# dirección dfu : 1d50:6017
# dirección de memoria : 0x08000000 pero se reservará los primeros bytes para gestores de arranque.. eso se verá en la siguiente sección.
```
#### **Grabado de firmware black_magic.bin por USB**
Ahora procedemos a conectar nuestro BMP (STM32 blue pill) al ordenador a través de su puerto microusb y ya no utilizando el STLINK.

![[Pasted image 20240915131254.png|ccbs]]

Ejecutar el siguiente comando de instalación de firmware (blackmagic.bin) por medio del utilitario dfu :
```shell
dfu-util -d 1d50:6017 -s 0x08002000:leave -D PATH/blackmagic.bin
	# iniciará indicadores de progreso de la instalación [0....100%]
```
#### **Detección de black_magic_probe**
Finalmente ya podremos comprobar si nuestro dispositivo stm32 es reconocido como un periférico depurador serial en nuestro ordenador : 
```shell
# listar los periféricos seriales
ls /dev/tty.*
	/dev/tty.usbmodem7EB87A971
	/dev/tty.usbmodem7EB87A973
	# otros periféricos más....

# listar los perifericos debugger de entrada
ls -l /dev/cu.usbmodem*
	crw-rw-rw-  1 root  wheel  0x900000d 15 sep 13:18 /dev/cu.usbmodem7EB87A971
	crw-rw-rw-  1 root  wheel  0x9000009 15 sep 13:18 /dev/cu.usbmodem7EB87A973
```
##### **Notas importantes sobre que puerto utilizar (tty.* o cu.* )**
Por lo general se utilizará los puertos de comunicación general ( cu.* ) para la grabación y depuración de código. Además de ello, se suele utilizar el primer puerto **`/dev/cu.usbmodem7EB87A971`**  para la comunicación del ordenador con el dispositivo (como la programación o la depuración a través de una interfaz como GDB), mientras que el segundo puerto está reservado para la interfaz **SWD** (Serial Wire Debug) o **JTAG**.
