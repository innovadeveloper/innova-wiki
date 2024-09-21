Este utilitario permite automatizar tareas para la compilación , enlace de ejecutables binarios 
#### Sintaxis

```shell
objetivo(s) : prerequisito(s)
    receta
    ...
```

##### Partes de una regla:

1. Objetivo(s): Es el archivo o archivos que se quieren generar o actualizar. Por ejemplo, puede ser un archivo ejecutable o un archivo objeto. También puede ser el nombre de una acción, como 'clean' (limpiar archivos innecesarios).

2. Prerequisito(s): Son los archivos de los que depende el objetivo. Si alguno de estos archivos ha cambiado, entonces el objetivo necesita ser actualizado. Por ejemplo, si el archivo fuente de un programa ha cambiado, el archivo objeto correspondiente debe ser recompilado.

3. Receta: Es el conjunto de comandos que Make ejecuta para generar o actualizar el objetivo. Cada línea de una receta debe comenzar con un carácter de tabulación (tab), que es un requisito importante en los Makefiles. Si no se utiliza tabulación, Make no sabrá que es una receta y generará un error. La receta es generalmente una serie de comandos de shell.
###### Ejemplos :

```shell

programa: archivo1.o archivo2.o archivo3.o
    gcc -o programa archivo1.o archivo2.o archivo3.o
```

```shell
clean:
    rm archivo1.o archivo2.o archivo3.o programa
```


#### Análisis de ficheros makefile

##### Makefile sin variables
```shell

edit : main.o kbd.o command.o display.o insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o insert.o search.o files.o utils.o

main.o : main.c defs.h
    cc -c main.c

kbd.o : kbd.c defs.h command.h
    cc -c kbd.c

command.o : command.c defs.h command.h
    cc -c command.c

display.o : display.c defs.h buffer.h
    cc -c display.c

insert.o : insert.c defs.h buffer.h
    cc -c insert.c

search.o : search.c defs.h buffer.h
    cc -c search.c

files.o : files.c defs.h buffer.h command.h
    cc -c files.c

utils.o : utils.c defs.h
    cc -c utils.c

clean:
    rm edit main.o kbd.o command.o display.o insert.o search.o files.o utils.o
```

###### Componentes :

1. Objetivo principal:
```shell
edit : main.o kbd.o command.o display.o insert.o search.o files.o utils.o
    cc -o edit main.o kbd.o command.o display.o insert.o search.o files.o utils.o
```

El objetivo principal es edit, el ejecutable que se quiere crear.

Los prerequisitos son los archivos objeto (.o) como main.o, kbd.o, command.o, etc. Esto significa que para crear edit, primero se necesitan estos archivos objeto.

La receta es el comando que usa el compilador cc para enlazar todos los archivos objeto y generar el ejecutable edit.



2. Reglas para compilar los archivos objeto: Cada archivo .o tiene una regla para definir cómo se compila a partir de su respectivo archivo fuente .c. Aquí hay un ejemplo de una de estas reglas:
```shell
main.o : main.c defs.h
    cc -c main.c
```

Esta regla indica que main.o depende de main.c y del archivo de encabezado defs.h. Si cualquiera de estos archivos cambia, main.o se recompilará.

La receta usa el comando cc -c main.c, que compila el archivo main.c en main.o.


De manera similar, hay reglas para compilar kbd.o, command.o, etc., cada una con sus propios archivos fuente .c y encabezados .h.


3. Objetivo clean:
```shell
clean:
    rm edit main.o kbd.o command.o display.o insert.o search.o files.o utils.o
```
clean es un objetivo falso (phony target), lo que significa que no genera un archivo. Su propósito es eliminar archivos generados, como el ejecutable edit y todos los archivos objeto .o, cuando se ejecuta el comando make clean.

La receta es el comando rm, que borra los archivos listados. Esto es útil para limpiar el directorio de compilación.

###### Notas :
- Para ejecutar la regla clean deberá ejecutarse explícitamente el comando "make clean"
- El proceso de construcción del objetivo principal desencadenará la ejecución de los demás objetivos (ficheros objetos)

##### makefile con variables
```shell
CC = cc
CFLAGS = -Wall
OBJ = main.o kbd.o command.o display.o insert.o search.o files.o utils.o

edit : $(OBJ)
    $(CC) -o edit $(OBJ)

main.o : main.c defs.h
    $(CC) $(CFLAGS) -c main.c

kbd.o : kbd.c defs.h command.h
    $(CC) $(CFLAGS) -c kbd.c
```

###### Formas de asignación de variables 

```shell
# Definir variables iniciales
CC = gcc
CFLAGS = -Wall -O2
DEBUG_FLAGS = -g -DDEBUG

# Concatenar variables usando +=
CFLAGS += -fPIC

# Concatenar al usar variables en recetas
ALL_FLAGS = $(CFLAGS) $(DEBUG_FLAGS)

# Regla de compilación
programa: main.o utils.o
    $(CC) $(ALL_FLAGS) -o programa main.o utils.o

main.o: main.c
    $(CC) $(ALL_FLAGS) -c main.c

utils.o: utils.c
    $(CC) $(ALL_FLAGS) -c utils.c
```

###### Sustitución de cadena de variables

```shell
SRC = main.c utils.c command.c
OBJ = $(SRC:.c=.o)
```

SRC contiene main.c utils.c command.c.

La expresión $(SRC:.c=.o) transforma cada archivo .c en un archivo .o, generando main.o utils.o command.o.

**Aplicación en recetas:**
```shell
programa: $(OBJ)
    gcc -o programa $(OBJ)
```

En este ejemplo:

$(OBJ) se expande a main.o utils.o command.o, que son los archivos objeto generados a partir de los archivos fuente.

###### Sustitución de cadenas de variables usando comodines 

```shell
SRC = src/main.c src/utils.c src/command.c
OBJ = $(SRC:src/%.c=obj/%.o)
```

Aquí estamos haciendo dos cosas:
1. Cambiando el directorio de src/ a obj/.
2. Cambiando la extensión de .c a .o.
**Explicación:**
**src/%.c**: Indica que estamos buscando archivos con el patrón src/ seguido de cualquier nombre de archivo (%) y con la extensión .c.

**obj/%.o**: Indica que queremos transformar ese patrón para que los archivos generados estén en el directorio obj/ y tengan la extensión .o.


###### tipos de variables expandidas

```shell
# variable expandida y es procesada en la compilación 

VAR := $(shell uname -s)

# variable recursivas son solo funciones hay un

OS := $(shell uname -s)

ifeq ($(OS), Linux)
    CC := gcc
else
    CC := clang
endif

all:
    $(CC) -o programa main.c
```
 Otro ejemplo más :
```shell
# Definición con expansión diferida
VAR1 = $(shell date)
# Definición con expansión inmediata
VAR2 := $(shell date)

print_vars:
    @echo "VAR1 = $(VAR1)"
    @echo "VAR2 = $(VAR2)"
```
Si ejecutamos "**make print_vars**" entonces mostrará :

```bash
VAR1 = (la fecha actual cuando se usa la variable)
VAR2 = (la fecha cuando se ejecutó la definición)
```
##### Uso de funciones útiles 
###### vpath & VPATH para realizar búsquedas de archivos en uno o más directorios
```shell
project/
├── include/
│   └── defs.h
├── src/
│   ├── main.c
│   ├── utils.c
└── Makefile
```
Y la forma de incluir todos los ficheros con vpath sería de esta manera :

```shell

# vpath permite realizar búsquedas usando comodines
vpath %.h include
vpath %.c src
# VPATH permite realizar búsqueda sin el uso de patrones 
VPATH = src:include

CC = gcc
CFLAGS = -Wall
OBJ = main.o utils.o

programa: $(OBJ)
    $(CC) -o programa $(OBJ)

main.o: main.c defs.h
    $(CC) $(CFLAGS) -c main.c

utils.o: utils.c defs.h
    $(CC) $(CFLAGS) -c utils.c
```
#### Flujo de trabajo del makefile

El orden en que GNU Make procesa las instrucciones es el siguiente:

1. **Lectura del Makefile**: Lee todo el Makefile de arriba hacia abajo antes de ejecutar cualquier comando.
2. **Expansión de variables**: Expande las variables en cuanto las encuentra, reemplazando las referencias de las variables con sus valores antes de seguir procesando.
3. **Definición de reglas y objetivos**: Asocia los objetivos con sus prerequisitos y recetas, pero aún no ejecuta nada.
4. **Determinación del objetivo principal**: Selecciona el primer objetivo del Makefile (o el que se especifique) como el principal.
5. **Verificación de dependencias (prerequisitos)**: Comprueba si los prerequisitos están desactualizados al comparar sus marcas de tiempo (timestamps).
6. **Ejecución de recetas**: Ejecuta las recetas en el orden necesario para actualizar los objetivos, empezando por los prerequisitos.


#### Definición de un makefile