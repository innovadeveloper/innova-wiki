##### Configuración del entorno



##### Importar un proyecto con compilador makefile

Tenemos de referencia el siguiente proyecto que contiene un fichero makefile en su raíz.

![[Screenshot_20240921-064151.jpg]]
El contenido del makefile
![[Screenshot_20240921-064158.jpg]]

Ahora le damos a eclipse : **New > Makefile project with existing code** 
![[Screenshot_20240921-062352.jpg]]
Seleccionamos la ruta del proyecto y elegimos el indexador correcto para el "arm"

![[Screenshot_20240921-063001.jpg]]
- Nota : Para el caso de desarrollo de microcontroladores arm, es crucial utilizar **Cros GCC** ya q de esa forma eclipse entenderá mejor nuestro código fuente y nos ayude con el auto completado, identificación de errores, etc.

##### Construir un proyecto a través de su makefile
Le damos click a la opción build del menú de acciones :

![[Screenshot_20240921-063726 1.jpg]]
- La herramienta de compilación 
![[Screenshot_20240921-064120.jpg]]

![[Screenshot_20240921-064137.jpg]]
- Se construyen los binarios