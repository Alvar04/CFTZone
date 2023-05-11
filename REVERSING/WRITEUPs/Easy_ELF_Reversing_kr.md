# RECONOCIMIENTO

Para empezar vamos a realizar un reconocimiento del CTF, para ello realizaremos una ejecucion de la aplicacion que nos proporciona el ejercicio.

<p align="center">
<image width="460" src="images/Run_Easy_ELF.png" caption="Ejecucion para el reconocimiento">
</p>

Como vemos simplemente el programa nos deja introducir una cadena de texto, realiza una comprobacion y nos indica en este caso "Wrong", con lo que tenemos que encontrar la cadena de texto correcta.

# ANALISIS DEL BINARIO

Para realizar el analisis del binario utilizaremos la herramienta Ghidra. Una vez abierto nuestro binario en Ghidra podemos analizar perfectamente el codigo, tanto en ensamblador como en C. El siguiente paso es encontrar la funcion en la que el binario realice la comparacion de lo que en principio introducimos por texto con los valores que deben ser los correctos. Una analizadas a simple vista las funciones encontramos la funcion o subrutina **FUN_08048451**

<p align="center">
<imageg width="480" src="images/FUN_08048451.png" caption="Funcion de compararion">
</p>


