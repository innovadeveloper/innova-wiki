En este **wikidoc** se presenta el siguiente alcance con el objetivo de mostrar como poder utilizar un STM32 (blue pill) para grabar firmwares en microcontroladores ARM tales como (STM32, Nrf52, otros) usando la interface SWD (también compatible con JTAG) y sustituirlo por el SeggerJLink.
**Alcances**
- Presentación del Black Magic Probe [[wd_BlackMagicProbe Presentación]]
- Servidor GDB y otras implementaciones (OpenCD) [[wd_ServidorGDB]]
- Requerimientos [[wd_Requerimientos Black Magic Probe]]
- Construcción y Grabado del firmware black_magic.duf.bin, black_magic.bin [[ws_Construcción y Grabado del firmware black_magic.duf.bin, black_magic.bin]]
	- Grabado de firmware black_magic.duf.bin por SWD
	- Grabado de firmware black_magic.bin por USB
	- Detección de black_magic_probe
- Black Magic Probe
	- Pinout in STM32 (BMP)
 ![[Pasted image 20240912164108.png|ccms]]
![[Pasted image 20240915133621.png|ccms]]	![[Pasted image 20240915133509.png|ccms]]
- (Pendiente) Construcción y compilación de una aplicación para STM32
	- Presentación del código
	- Compilación del artefacto
- Grabando artefacto "elf" al stm32 usando el BMP [[wd_Black Magic Probe Grabador de firmware]]
