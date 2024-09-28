##### Configuración del entorno

- Descargar e instalar en el sistema la cadena de herramientas de compilación 
	- https://developer.arm.com/downloads/-/gnu-rm
- Descargar e instalar Eclipse Embedded for CC Developers
	- https://www.eclipse.org/downloads/packages/release/2024-09/r/eclipse-ide-embedded-cc-developers
	- Más info :
		- https://eclipse-embed-cdt.github.io/plugins/install/
		- Ese ide ya incluye :
			- the **Eclipse IDE for C/C++ Developers** standard distribution with the **Eclipse Embedded CDT plug-ins**
- Descargar e instalar plugin GNU MCU Eclipse Plugin a través del market place de Eclipse : 
	- ![[Screenshot_20240921-081314.jpg|ccbs]]
	- ![[Screenshot_20240921-081348.jpg|ccbs]]
	- ![[Screenshot_20240921-074202.jpg|ccbs]]
- Configurar el tool chain en eclipse :
	- Ve a **Window > Preferences > C/C++ > Build > Global Tools Paths**.
	- Agrega la ruta al compilador arm-none-eabi-gcc en la sección Cross GCC Toolchain Path.

##### Importar un proyecto con compilador makefile

Tenemos de referencia el siguiente proyecto que contiene un fichero makefile en su raíz.

![[Screenshot_20240921-064151.jpg|ccbs]]
El contenido del makefile
![[Screenshot_20240921-064158.jpg|ccbs]]

Ahora le damos a eclipse : **New > Makefile project with existing code** 
![[Screenshot_20240921-062352.jpg|ccbs]]
Seleccionamos la ruta del proyecto y elegimos el indexador correcto para el "arm"

![[Screenshot_20240921-063001.jpg|ccbs]]
- Nota : Para el caso de desarrollo de microcontroladores arm, es crucial utilizar **Cros GCC** ya q de esa forma eclipse entenderá mejor nuestro código fuente y nos ayude con el auto completado, identificación de errores, etc.

##### Construir un proyecto a través de su makefile
Le damos click a la opción build del menú de acciones :

![[Screenshot_20240921-063726 1.jpg|ccbs]]
- La herramienta de compilación 
![[Screenshot_20240921-064120.jpg|ccbs]]

![[Screenshot_20240921-064137.jpg|ccbs]]
- Se construyen los binarios