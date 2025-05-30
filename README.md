# Macro para iniciar en las macros - Polyworks Macro Script
## _Repositorio de macros simples para polyworks_

### Codigo ayuda para empezar con macros en Polyworks
Dentro de poliworks se utiliza un lenguaje de programacion MSCL (Lenguaje de Control de Macro Script) 

##Descripcion de macro
```mscl
version "5.0"
# linea de version, hace referencia a la version de codigo macro a utilizar para iniciar
#a programar las sentencias y operaciones a utilizar en la macro.
############################## POLYWORKS ######################################
#
# ---- InnovMetric Software Inc.
# ---- Module  :    PolyWorks|Inspector
# ---- Version :    2020 (build 2255)
# ---- Date    :    Wednesday, March 25, 2020 - 13:57:52
#
############################## DESCRIPCION ####################################
# 
#Esta macro es un buen punto de partida para desarrollar tus habilidades de
#programación con el lenguaje de comandos de script de macros de PolyWorks (MSCL).
#Te enseña los conceptos básicos para crear tus propias macros, con una buena
#combinación de explicaciones y ejemplos.
#
```

##Desgloce de codigo
``` mscl
############################## Codigo ###########################################
#
#      Para comprender mejor el desgloce del codigo y la funcion de cada linea,
#      puede activar la ventana de historial de comando
#
# Command History (Tools -> Commands -> Command History)
#
# ------------------------------------------------------
#     Cada operación realizada en PolyWorks escribirá un comando
#     correspondiente en el historial de comandos.
#     Estos comandos son los componentes básicos de las macros.

# Macro Script Editor (Tools -> Macro Scripts -> Macro Script Editor)
# --------------------------------------------------------------------
#
#    Este editor de texto te permite escribir y ejecutar tus propias macros.
#    Puedes copiar y pegar fácilmente comandos del Historial de comandos
#    en el Editor de scripts de macros.

WINDOW VIEW ( "Command History", "On" )


#    Comando "Echo"
# -----------------------------------------------------------
# Este comando nos permite mostrar informacion al usuario, esta siendo de 2 formas diferentes
# MACRO ECHO: Este comando enviará información al Historial de comandos
# MACRO PAUSE: Este comando mostrara un mensaje en una ventana emergente con la informacion
# 
# Comillas: Tenga en cuenta que las comillas "" son necesarias cuando se utiliza texto

MACRO ECHO ( "Hello World." )
MACRO PAUSE ( "Hi", "Hello Earth." )


# Variables
# -------------------------------------------------------------------
# Las variables se usan para almacenar información (imagínate un contenedor o un depósito).
# Puedes introducir información dentro del contenedor o extraerla para usarla.
#
# DECLARE: Para que ese contenedor exista, primero debe declararse
# SET: Usa este comando para asignar un valor a una variable, una vez declarada. #
# También puede establecer el valor de las variables agregando el valor después del nombre de la variable (opcional).
#
# $: Necesario si desea usar el valor de una variable (OUT).
# {}: Necesario para aislar una variable dentro de una cadena de texto.
#
# Tipos de variables (detectadas automáticamente, no es necesario especificar):
# - INTEGER: Número entero (sin punto decimal).
# - DOUBLE: Número que permite puntos decimales.
# - STRING: Lista de caracteres alfanuméricos.
#
# Modificadores de variables
# :l Minúsculas.
# :u Mayúsculas.
# 
# Variables reservadas
# - _PI (3.14159...)
# - El script cuenta con muchas otras variables que empiezan con un guión bajo "_".
#
# Puede pasar el ratón por encima de las variables para conocer su valor o valores.
# Igual al pasar el raton sobre lineas de codigo incompletas o con informacion faltante puede conocer el tipo de estructura que debe llevar
# o el tipo de informacion que se debe usar para terminar la linea de codigo  

#Declaracion de variables
DECLARE variable1 "Message 1"
DECLARE variable2 
DECLARE a 1
DECLARE b

#Asignacion de valores a variables
SET variable2 "Message 2"
SET b 2

#Mostrar informacion en historial de comandos 
MACRO ECHO ( $variable2 )
#Mostrar informacion en una ventana emergente
MACRO PAUSE ( "Use Variable", $variable1 )


MACRO ECHO ( "Message = $variable2" )
MACRO PAUSE ( "Followed", "$variable2 followed by extra words" )
MACRO PAUSE ( "Isolate", "${variable2}345 closely followed by extra numbers (345), and then words" )

MACRO PAUSE ( "PI", "Pi = ${_PI}" )
MACRO PAUSE ( "Uppercase", "$variable1 Uppercase = ${variable1:u}" )


# Expresiones Matematicas
# -------------------------------------------------------------------------------
# EXPR: Calcula una ecuación para establecer un valor
# EXPR_I: Calcula una ecuación y conserva la parte entera del resultado (sin redondeo)
# +, -, *, /, % (Modulo):Operadores aritméticos disponibles en ecuaciones
# ABS (Absolute), SQRT (Square Root), SIN, COS, TAN, etc. : otros operadores

DECLARE c
DECLARE d
DECLARE e

SET c EXPR ( $a + $b )
SET d EXPR ( SQRT( $c ) )
SET e EXPR_I ( SQRT( $c ) )

MACRO PAUSE ( "Math", "$a + $b = $c", "Square Root of $c = $d", "Square Root of $c (no decimals) = $e" )


# Expresiones Logicas
# -------------------------------------------------------------------------------
# Puede utilizar expresiones lógicas (condiciones) para realizar un procesamiento particular.
#
# IF:     Iniciar la declaración condicional
# ELSEIF: Agregar condiciones alternativas
# ELSE:   Indique una alternativa para los casos donde todas las condiciones IF o ELSEIF son falsas
# ENDIF:  Detener la declaración condicional
#
# Operadores de comparacion:
#   < Menor que
#   <= Menor que o igual a
#   > Mayor que
#   >= Mayor que o igual a
#   == Igual a
#   != Diferente de
# 
# Operadores logico:
#   AND (Las 2 condiciones son verdaderas)
#   OR  (al menos una o las dos condiciones deben ser verdaderas)
#   NOT (invertir la logica)

#Ejemplo de sentencia "Si"
IF $c == 0
    MACRO PAUSE ( "Zero", "$c equals zero." )
ELSEIF $c < 0
    MACRO PAUSE ( "Smaller than zero", "$c is negative (<0)." )
ELSE
    MACRO PAUSE ( "Bigger than zero", "$c is positive (>0)." )
ENDIF

IF $a > 0 AND $b > 0
    MACRO PAUSE ( "Bigger than zero", "$a AND $b are both bigger than zero." )
ENDIF

IF $a > 0 OR $b > 0
    MACRO PAUSE ( "Bigger than zero", "$a OR $b is bigger than zero." )
ENDIF

# Arrays = "Matrices"
# -------------------------------------------------------------------------------
# Los valores múltiples asignados a una sola variable se denominan matriz.
# El primer valor de esa matriz es la variable[1] (el segundo valor es la variable[2]).
#
# Size: Obtenga el número de valores presentes en la matriz de variables.
# {}: Útil para declarar una matriz

DECLARE Modulos { "Inspeccion", "Modelador", "IMAlineacion", "IMFusion" }
DECLARE ModulosSize SIZE( Modulos )
MACRO PAUSE ( "Main modules", "The $ModulosSize main modules of PolyWorks are: $Modulos[1], $Modulos[2], $Modulos[3] and $Modulos[4]" )

# Loops = "Bucles"
# -------------------------------------------------------------------------------
# Los bulces son usados ara repetir pasos o procesos.
#
# WHILE: inicia el bucle
# ENDWHILE: detiene (termina) el bucle
# BREAK: finaliza la repeticion del bucle
# CONTINUE: Continuar fuera del bucle repetitivo
#
# WHILE Los bucles pueden usar un contador (por ejemplo, "i") para contar los ciclos a través del bucle.
# Una vez que el contador alcanza su valor indicado, el bucle se detiene.
#
# ++: Incrementa el valor de las variables (same as: SET i EXPR ( $i + 1 ) )
# --: Decrementa el valor de las variables (same as: SET i EXPR ( $i - 1 ) )

DECLARE PolyWorksIter 1
WHILE $PolyWorksIter <= $PolyWorksSize
    MACRO ECHO( "PolyWorks Module $PolyWorksIter = $PolyWorks[$PolyWorksIter]" )
    
    ++ PolyWorksIter
ENDWHILE 

# Ingresar un valor, comando "Input"
# --------------------------------
# Puede interactuar con el usuario para obtener información.
#
# Question:  Yes/No question (returns 1 for yes or 0 for no)
# Directory: Buscar una direccion en el directorio de la computadora
# File_Path: Buscar un archivo
# Double:    Ingresar un valor con decimales
# Integer:   Ingresar un valor entero
# String:    Ingresar un valor de tipo caracter o cadena de caracteres
# Multiple:  Ingresar valores de multiples parametros (Los argumentos pueden ser entero, fotante(doble),string, en el orden que quiera) (arguments: 1-type, 2-label, 3-default value)
# Note: los parametros del comando de variables multiple deben ser siempre en esos 3 tipos.
#
#Más modificadores de variables
#   :e Mantener el sufijo o extraer la extension (ejemplo: .pdf) 
#   :r Remover el sufijo o la extencion 
#   :h Mantener el directorio o el nombre 
#   :t Remover el directorio o el nombre 

DECLARE answer
MACRO INPUT QUESTION ( answer, "Click on YES or No" )

IF $answer == 1
    MACRO PAUSE ( "Question", "You clicked: YES" )
ELSE 
    MACRO PAUSE ( "Question", "You clicked: NO" )
ENDIF 

DECLARE fileName
MACRO INPUT FILE_PATH ( fileName, "Browse for a File" )
MACRO PAUSE ( "File", "The FILE is: $fileName", "The file PATH is: $fileName:h", "The file EXTENSION is: $fileName:e", "The file NAME is: $fileName:t:r" )

DECLARE folderName
MACRO INPUT FOLDER_PATH ( folderName, "Select a Folder", )
MACRO PAUSE ( "Folder", "The folder path is: $folderName" )

DECLARE name "John"
DECLARE age "35"
DECLARE height "1.65"
MACRO INPUT MULTIPLE_PARAMETERS ( "Multiple Parameters", "About you:",\
    {"String", "    Name", $name,\
    "Integer", "    Age", $age,\
    "Double", "    Height", $height},\
    name, age, height )
MACRO PAUSE ( "About You", "$name is $age years old (${height}m tall)." )


# Archivos de texto
# ---------------------------------------------
# Se pueden escribir y leer archivos de texto. Al leer un archivo de texto, se puede leer una línea.
# a la vez, o todos a la vez y almacenados en una matriz para cada columna de archivo.
#
# Mas variables reservadas:
#   - _TEMP_PATH: Temporary folder (will get deleted upon rebooting)
#   - _PWK_FILES_PATH: Folder inside the Workspace (will travel along with a project)

DECLARE textFileName "${_PWK_FILES_PATH}\user-data\Text_File_Name.txt"
DECLARE textFileFields
DECLARE textFileLineNb
DECLARE textFileLineIter

DATA_FILE CREATE ( $textFileName, "Ascii", "Yes" )
DATA_FILE APPEND LINES ( $textFileName, "John,Lennon" )
DATA_FILE APPEND LINES ( $textFileName, "Paul,McCartney" )
DATA_FILE APPEND LINES ( $textFileName, "Ringo,Starr" )
DATA_FILE APPEND LINES ( $textFileName, "George,Harrison" )

DATA_FILE PROPERTIES NB_LINES GET ( $textFileName, textFileLineNb )

SET textFileLineIter 1
WHILE $textFileLineIter <= $textFileLineNb
    DATA_FILE READ LINE_FIELDS ( $textFileName, $textFileLineIter, textFileFields, ",", "On" )
    
    IF $textFileFields[1] == "Ringo"
        MACRO PAUSE ( "Data File", "$textFileFields[1] is a ${textFileFields[2]}!" )
        BREAK
    ENDIF
    
    ++ textFileLineIter
ENDWHILE


DECLARE firstName
DECLARE lastName
SET textFileLineIter 1

DATA_FILE READ COLUMNS ( "${_PWK_FILES_PATH}\user-data\Text_File_Name.txt", ",", "Off", 1, 4, firstName, lastName )
DATA_FILE CREATE ( "${_PWK_FILES_PATH}\user-data\Text_file_paul_only.txt", , )
WHILE $textFileLineIter <= 4
    IF $firstName[$textFileLineIter] == "Paul"
        DATA_FILE APPEND ( "${_PWK_FILES_PATH}\user-data\Text_file_paul_only.txt", "$firstName[$textFileLineIter] $lastName[$textFileLineIter]", )
    ENDIF
    ++ textFileLineIter
ENDWHILE

```
