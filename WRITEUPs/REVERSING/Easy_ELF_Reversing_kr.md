# RECONOCIMIENTO

Para empezar vamos a realizar un reconocimiento del CTF, para ello realizaremos una ejecucion de la aplicacion que nos proporciona el ejercicio.

<p align="center">
<image width="460" src="images/Run_Easy_ELF.png" caption="Ejecucion para el reconocimiento">
</p>

Como vemos simplemente el programa nos deja introducir una cadena de texto, realiza una comprobacion y nos indica en este caso "Wrong", con lo que tenemos que encontrar la cadena de texto correcta.

# ANALISIS DEL BINARIO

Para realizar el análisis del binario utilizaremos la herramienta Ghidra. Una vez abierto nuestro binario en Ghidra podemos analizar perfectamente el código, tanto en ensamblador como en C. El siguiente paso es encontrar la funcion en la que el binario realice la comparación de lo que en principio introducimos por texto con los valores que deben ser los correctos. Una vez analizadas a simple vista las funciones encontramos la función o subrutina **FUN_08048451**

<p align="center">
<image width="500" src="images/FUN_08048451.png" caption="Funcion de compararion">
</p>
  
Como podemos ver en la función tenemos una varaibles que pertenecen a posiciones de memoria con el formato de nombre **DAT_0804a021**. Observando, vemos que se realiza una operacion del lenguaje de C, es una **XOR** que corresponde con el símbolo (^) entre los valores que haya en las posiciones de memoria y los valores hexadecimales. Si esas operaciones pasan las sucesivas comprobaciones en de los if, tendremos un 1 en la variable **uVarl** y si alguna falla tendremos un 0.
  
# OBTENCION DEL PASSWORD

Realicemos las operaciones XOR:
  
<p align="center">
<image width="500" src="images/XOR_Operaciones.png" caption="Resultados de las XOR">
</p>

En la tabla tenemos 4 filas:
  - Posición de memoria.
  - Dato: es el dato en binario y hexadecimal con el que se realiza la XOR.
  - Resultado: es la solucion que tiene que dar de la XOR entre el dato y el valor scanf.
  - Valor Scanf: es el valor que introducimos por texto nosotros, y es el que queremos averiguar.

De esta manera realizando la operacion entre Dato y el supuesto valor de Scanf para que nos de cada uno de los bits de Resultado.
  
También tenemos otras posiciones de memoria aparte de las de la tabla:
  - Posición 21: que tiene que llevar un 1, primer if de la función.
  - Posición 24: que tiene que llevar una X, segundo if de la función.
  - Posición 25: que tiene que llevar un '\0', es decir, un final de línea.
  
La posición 25 nos da la clave para averiguar nuestra contraseña, ya que si es un final de línea, este debería ir al final, con lo que vemos que hay que ordenar las posiciones de memoria para poder sacar la contraseña:
  - Posición 20: el valor en hex. es 4C que en decimal es 76, cuyo caractér correspondiente en ASCII es 'L'.
  - Posición 21: que tiene que llevar un 1, primer if de la función.
  - Posición 22: el valor en hex. es 4E que en decimal es 78, cuyo caractér correspondiente en ASCII es 'N'.
  - Posición 23: el valor en hex. es 55 que en decimal es 85, cuyo caractér correspondiente en ASCII es 'U'.
  - Posición 24: que tiene que llevar una X, segundo if de la función.
  - Posición 25: que tiene que llevar un '\0', es decir, un final de línea.
 
**SOLUCIÓN**= nuestras password es L1NUX.
