# Tipos de datos en JavaScirpt

## Qué son los tipos de datos

Los tipos de datos en un lenguaje de programacion son las caracteristicas que posee un dato, por ejemplo, los numeros pueden ser usados en funciones matematicas, los booleanos permiten ejecutar un código si se cumple una condición, además, cada tipo de dato puede ser manipulado de diferentes maneras.

## JavaScript: un lenguaje débilmente tipado

Un lenguaje de programación puede clasificarse por la forma en que permite combinar los diferentes tipos de datos, por ejemplo combinar números con strings o reasignar variables con otros tipos de datos.

Por ejemplo, C es un lenguaje fuertemente tipado y para escribir textos debes indicar el tipo de dato y cuantos bytes va a utilizar el texto, y es imposible que la variable que usaste para guardar el texto cambie de tipo de dato o la cantidad de byts que utiliza.

JavaScript es un lenguaje débilmente tipado, lo que significa que podemos, por ejemplo, combinar strings con números, booleanos, o con cualquier otro tipo de dato, o asignar a las variables distintos tipos de datos en distintos momentos realiza el siguiente experimento, intenta sumar un string con cualquier otro tipo de datos.

Como experimento intenta sumar un string con cualquier otro tipo de dato en JavaScript.

      console.log(5 + "Some") // "5Some"
      console.log("Some" + [12]) // "Some12"

Todo esto varía según el lenguaje de programación, sin embargo JavaScript es un lenguaje peculiar en el que la siguiente imagen es posible:

![Es posible que hacer "2" + "2" - "2" = 20, o que "2" + "2" = "22"](https://firebasestorage.googleapis.com/v0/b/web-projects-50e7e.appspot.com/o/images%2Fv2%2Fblogs%2Ftipos%20de%20datos%2Fjs-data-tipes-meme.png?alt=media&token=6c551e2b-1bab-4f65-b5ad-92e64d3e451c)

## Numbers

El tipo de dato Number es cualquier número, ya sea entero o decimal, positivo o negativo. Ya que los números son infinitos JavaScript tiene un límite de qué números pude representar, para saber cuál es el número más grande que puede ser representado en JavaScript solo debes ejecutar:

      // Número positivo máximo
      console.log(Number.MAX_VALUE)

      // Número negativo mínimo
      console.log(Number.MIN_VALUE)

## Strings

Los strings son una sucesión de caracteres(letras, números o símbolos), ahora, una duda común es ¿Cuál es la diferencia entre representar un número como el tipo de dato "Number" y utilizarlo en strings?:

1. Los métodos:

   - Números:

     Los números en JavaScript solo tienen métodos para ser convertidos a string u obtener el valor del número

   - Strings:

     Los strings pueden ser convertidos a mayúsculas, minúsculas, a número (si el carácter es el usado para representar un número), puede obtenerse cuántos caracteres tiene el string.

### Formas de escribir strings

Los strings pueden escribirse de tres formas:

- Usando comillas dobles: Se usa "", es la forma más simple de utilizarlos, su inconveniente es que no puedes usar un string con comillas dobles dentro (" "" "), es necesario usar comillas simples.
- Usando comillas simples: Se usa '', su inconveniente es que no puedes usar un string con comillas simples dentro (' '' '), es necesario usar comillas dobles.
- Template literals: Se usa: ``. Es la forma más versátil de crear strings, puedes usar cualquier comilla (excepto template literals), permite utilizar otros tipos de datos dentro del string, es útil cuándo [quieres hacer un server side render (ssr) simple](https://ulisessg.com/crea-tu-ssr), cuando quieres escribir párrafos,

## Boolean

Los booleanos son datos que representan si algo es verdadero o es falso, por lo que solo existe **true** y **false**. Son útiles cuándo queremos saber si existe un valor dentro de un objeto:

      if('some' in object) {
            doSomething()
      } else {
            doSomethignElse()
      }

## Null

Null es el valor utilizado para indicar que no hay nada en una variable, es literalmente "No hay nada".

## Undefined

Es el valor que toman las variables cuando están declaradas, pero no almacenan ningún dato, por ejemplo:

      var x;
      console.log(x)
      // Imprime undefined

## Symbol

Symbol te permite crear datos inmutables (que nunca cambien) o de difícil acceso, esto es útil por ejemplo cuando queremos que un valor dentro de un objeto no pueda modificarse. La única forma de acceder a ese valor es con el identificador, la forma de crear un dato inmutable con Symbol es:

      const identificador = Symbol('Descripción opcional de que es este Symbol')
      var obj = {
        // Así es como podemos usar el Symbol dentro del objeto
        [identificador]: 12
      }

Para poder acceder al valor del Symbol debes:

      console.log(obj[identificador])
      // Si intentas hacerlo de cualquier otra forma el valor será undefined.

Existe solo una forma de poder modificar el valor de **x**, sin embargo no es óptimo modificar este valor, ya que la idea principal es que nadie pueda acceder a el:

      obj[x] = 21

## Object

Los objetos en programación forman parte de la POO(programación orientada a objetos), en la que buscamos que un objeto represente a un elemento de la vida real, esto lo hacemos con una estructura de "llave - valor", siendo la llave una forma de identificar el dato al que queremos acceder, por ejemplo el objeto una persona:

      const person = {
        // Nombre y edad son las llaves
        nombre: "Luis",
        edad: 24
      }

Si observas el objeto person tiene dos llaves (nombre y edad), y los valores son tipos de datos que ya hemos visto.

Para acceder a los valores dentro de un objeto hacemos:

      console.log(person.nombre)
      // Esto imprimirá "Luis"

## Lecturas recomendadas

- [Tipos de datos y estructuras en JavaScript, MDN](https://developer.mozilla.org/es/docs/Web/JavaScript/Data_structures)

- [websarrolladores.com](https://websarrolladores.com/lenguajes/javascript/manual-completo-javascript/tipos-de-datos-javascript/)
