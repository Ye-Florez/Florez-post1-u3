# Laboratorio: Exploración con DEBUG en DOSBox
# Unidad 3 -- Post Contenido 1 | Arquitectura de Computadores

**Estudiante:** Florez
**Repositorio:** apellido-post1-u3  

## Proposito del Laboratorio
Este laboratorio tiene como objetivo configurar el entorno de DOSBox y utilizar el depurador DEBUG  
para inspeccionar registros del procesador, manipular bloques de memoria y desensamblar código 
en modo real x86. 
Se emplean los comandos R, D, F y U para documentar el comportamiento 
interno del procesador a nivel de hardware.

## Checkpoint 1  — Estado de registros
Comando: R

Este comando muestra el estado completo del procesador al iniciar DEBUG.
Se observa que los registros de propósito general AX, BX, CX y DX se encuentran en cero, 
indicando que no hay operaciones previas en memoria.
Los cuatro registros de segmento (DS, ES, SS, CS) apuntan al mismo valor,
correspondiente al segmento del PSP asignado por el sistema operativo DOS.
El registro IP se encuentra en 0100, que representa la primera dirección
ejecutable después del PSP.

Posteriormente se modifica el registro AX con el valor 1234 usando el 
comando R AX, lo que demuestra que DEBUG permite alterar el estado 
del procesador de forma selectiva sin afectar los demás registros.

## Checkpoint 2  — Volcado de Memoria 
Comando: F - D

Se rellenan 64 bytes a partir de la dirección DS:0200 con el patrón AB CD EF usando el 
comando F 200 L40 AB CD EF. El patrón se repite cíclicamente hasta completar el bloque.

El comando D 200 L40 muestra la región rellena. 
La salida se organiza en tres columnas:
Columna 1: indica la dirección de memoria en formato segmento:offset donde comienza cada fila.

Columna 2:  muestra 16 bytes por fila en formato hexadecimal, separados en dos grupos de 8
por un guion central.

Columna 3: representa los mismos bytes como caracteres. Los bytes AB, CD y EF aparecen como
puntos porque están fuera del rango ASCII imprimible (0x20–0x7E).

## Checkpoint 2  — Volcado de Memoria 
Comando: A - U

Se ensambla un programa de 4 instrucciones en CS:0100 usando el comando A 

MOV AX, 0005 --  Carga el valor 5 en el registro AX 

MOV BX, 0003 --  Carga el valor 3 en el registro BX

ADD AX, BX   --  Suma BX a AX, resultado en AX

INT 20       --  Termina el programa 

El comando U 100 109 verifica que el ensamblado fue correcto mostrando 
la correspondencia entre mnemónicos y bytes de código máquina. 

## Conclusiones 
El laboratorio permite comprender que en el modo real x86 no existe distinción entre código 
y datos: el procesador interpreta como instrucción cualquier byte al que apunte el registro 
CS:IP. Los bytes 00 00 son interpretados como la instrucción ADD [BX+SI],AL, lo que demuestra 
que la arquitectura x86 no protege regiones de memoria por tipo.

El depurador DEBUG se vuelve una herramienta fundamental para observar el comportamiento interno
del procesador, modificar registros y memoria en tiempo real, y verificar el resultado del
ensamblado a nivel de bytes.

