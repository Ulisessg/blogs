# Scope en JavaScript

El scope en JavaScript es el alcance que tienen las variables, o dicho en palabras más sencillas: en qué bloques de código puedo  acceder a una variable, por ejemplo una regla del scope es que no puedo utilizar una variable antes de que esta sea declarada:

```javascript
  console.log(x) // Esto va a generar un error, ya que estamos utilizando la variable "x" antes de que esta sea declarada
  const x = 12
```

## Tipos de scopes

El scope es el alcance que tienen las variables y este alcance está definido según el bloque de código en el que están declaradas (aunque aún no tengan un valor aún), por ejemplo:

### Scope global

Son todas aquellas variables que pueden ser accedidas en cualquier parte del programa, la principal variable global es _window_ en el caso de los **navegadores** y _global_ en el caso de **Node.js**.

Sin embargo **es mala práctica declarar variables en el scope global**, ya que puede aumentar la probabilidad de que ocurran errores como:

- Afectar de forma inesperada a funciones o módulos que dependan de ella

- Hacer más complejo la lectura del código

Como las variables globales pueden ser accedidas desde cualquier parte del programa, también pueden ser modificadas desde cualquier parte del programa, por lo que si hay un bug que cambia de forma inesperada el valor de la variable será más difícil saber dónde fue cambiado el valor y tendrás que ir a cada parte del programa que la modifica para saber dónde fue.

- No tener acceso a ella si declaramos una **variable local** con el mismo nombre

**Se habla más a profundidad de esto en el scope de función**

- Dificultar la creación de tests

Cuando estamos creando tests para nuestros programas buscamos probar cada parte del programa de forma aislada, y la existencia de variables globales hace que más partes del código dependan de otras para funcionar. 

- Dificultar la separación de del código en bibliotecas 

Algunos sistemas que utilizan bibliotecas (como DLL), no permiten acceder de forma directa ni transparente a las variables globales por lo que será difícil acceder a ese valor o incluso casi imposible.

### Scope de bloque

Para entender esto mejor abre una pestaña de tu navegador y abre la consola (CTRL + MAYUSC + I) y corre este código:

```javascript
let a = 12;
{
	const x = 0;
}

console.log(x); // Uncaught ReferenceError: x is not defined

```

El código anterior genera un error, ya que la variable **x** es declarada en un scope diferente al scope global, a esto lo llamamos scope de bloque.

Las variables declaradas dentro de un bloque de código solo pueden ser accedidas dentro de ese bloque de código o en los bloques de código que sean descendientes de este.


Se considera que una variable está dentro de un scope de bloque cuando son declaradas (se inicializan) dentro de un ciclo, un if statement, un bloque de código, un módulo o dentro de una función.


### Scope de función

En las funciones existe otro scope especial que es el de función.

En este scope las variables son declaradas en los parámetros de la función, por lo tanto estas variables solo existen en el bloque de código que hay en la función.

Cuando una función tiene parámetros, internamente en el navegador ocurre esto

```javascript
function x (let j, let k) { 
	return j + k
}

// Esto es solo una forma de verlo, si intentas ejecutar este código se va a generar un error

```

Como hablé en los puntos de por qué es mala práctica tener variables globales, cuando una variable global tiene el mismo nombre que un parámetro de la función, solo podremos tener acceso a la variable global y nunca vamos a poder acceder a la variable declarada en los parámetros, esto es especialmente problematico, ya que se pierde la principal utilidad de las funciones que es repetir código con información que dependa de un contexto.


Ahora que ya sabes un poco mejor qué es el scope y los tipos que hay, te va a ser útil saber cómo JavaScript sabe cuál es el scope de cada variable, para esto te será útil entender cómo pasa nuestro código de la sintaxis de JavaScript a algo que puede entender una computadora

## Cómo es JavaScript


Cada lenguaje de programación se basa en diferentes paradigmas (formas ya probadas y fiables de hacer las cosas) y uno de los más importantes es el tipo de proceso que hace que nuestro programa pasa de una sintaxis legible para humanos a algo que pueda entender una computadora (byte code o código de máquina).

Para eso existen 2 formas de hacerlo, compilando o interpretando el código, en el caso de javascript se lleva a cabo un proceso de interpretación y después de compilación (mejor conocido como 'Just in time compiler').

## Compilación vs interpretación

Recordemos los lenguajes de programación que generalmente usamos son de alto nivel (son fácilmente entendibles por seres humanos), pero nuestras computadoras solo entienden código binario o byte code (que es un lenguaje de bajo nivel) por lo que nuestro código debe pasar por un proceso de interpretación o compilación para pasar de un lenguaje de alto nivel a uno de bajo nivel.

En ambos casos el código resultante va a ser un código entendible por las computadoras, pero el proceso es distinto.

### Compilación

En la compilación siempre debemos esperar a que todo nuestro código sea compilado en un archivo nuevo para que podamos probar el resultado.

### Interpretación

En un lenguaje interpretado el proceso de compilación se hace línea por línea, cuando una parte del código termina de ejecutarse la siguiente comienza a hacerlo.

Recuerda que JavaScript funciona en el navegador y en el servidor, pero cada navegador tiene su propio motor de JavaScript y Node utiliza el propio (basado en V8 que es el motor open souce que usa Chrome)

En el caso de JavaScript nuestro código es primero parseado y compilado antes de ser ejecutado.

## Proceso de compilación en JavaScript

Para entender el scope de JavaScript es esencial entender cómo funciona su proceso de compilación.

Existen multiples formas en las que se puede llevar a cabo el proceso de compilacion, pero en la forma clásica requiere de 3 pasos:

1. Tokenización: en este paso el motor de JavaScript busca cada una de las palabras clave que utiliza el lenguaje y los caracteres que pueden ser importantes

Por ejemplo, en la creación de una variable se divide cada elemento en un token:

const age = 12; => [const][age][=][12][;]

Es durante este proceso en el que se suelen detectar los errores de sintaxis, ya que si el motor detecta palabras que no conoce o que no han sido inicializadas como una variable va a generar un error (Unexpected token, Keyword reservated, etc.) 

2. Parseo: En este paso se toma una lista(array) de tokens y se convierten en un árbol de tokens anidados, y a la suma total de esos árboles de tokens anidados se les llama <p lang="en">Abstract Syntax Tree</p> (AST), este árbol es básicamente un JSON en el que se describe la relación entre tokens:

Del siguiente código:

const x = 12;


va a salir el siguiente JSON:

```json
{
  "type": "Program",
  "start": 0,
  "end": 13,
  "body": [
    {
      "type": "VariableDeclaration",
      "start": 0,
      "end": 13,
      "declarations": [
        {
          "type": "VariableDeclarator",
          "start": 6,
          "end": 12,
          "id": {
            "type": "Identifier",
            "start": 6,
            "end": 7,
            "name": "x"
          },
          "init": {
            "type": "Literal",
            "start": 10,
            "end": 12,
            "value": 12,
            "raw": "12"
          }
        }
      ],
      "kind": "const"
    }
  ],
  "sourceType": "module"
}
```


Si quieres explorar por tu cuenta cómo ocurre con tu propio código puedes usar la página [AST explorer](https://astexplorer.net/)

Cuando el AST está creado es un poco más fácil entender cómo JavaScript accede a cada variable dependiendo de su scope, si una variable no ha sido declarada es imposible que el navegador acceda a una parte del JSON que aún no ha sido creada, ya que el código se ejecuta despues de que el código anterior termina de hacerlo


### Errores comunes detectados en el parseo:

- ReferenceError: Ocurre cuando se utiliza una variable que aún no ha sido declarada

```javascript
const x = 23

console.log(y) // Aquí se detecta que nunca se ha declarado la variable "y"
```
- SyntaxError: Es el tipo de error más común y se genera cuando se utilizan tokens o caracteres que no deberían estar ahí, por ejemplo:

```javascript
const x = 23

console.log(.x)// Aquí el punto antes de la x no debería estar, ya que no tiene ningún tipo de sentido ahí
```

- TypeError: Ocurre cuando intentamos utilizar un método que no existe dentro de un [tipo de dato](https://ulisessg.com/tipos-de-datos), por ejemplo:

```javascript
const list = [1,2,3]

list.toUpperCase() // El método toUpperCase() solo existe en los strings.

```
 
3. Generación de código: A partir del AST se genera el código binario que puede entender una computadora


## Haciendo trampa: modificando el scope durante la compilación

Como puedes ver el scope es creado al momento de crear el AST, sin embargo existen 2 formas de romper estas reglas del scope y elevar variables a un scope más alto.

Solo toma en cuenta que es peligroso hacer esto no solo porque representa riesgos de seguridad, sino que hace más confuso entender el código.

### Eval

Eval es una función global de JavaScript que permite ejecutar código en el scope global utilizando un string, si bien esto puede sonar interesante lo cierto es que abre un hueco de seguridad enorme si se utiliza en partes donde el usuarix puede modificar el string que se ejecuta, ya que ese código tiene el mismo nivel de privilegios que tiene nuestro código.

Para probarlo puedes ejecutar el siguiente código:

```javascript
function badIdea() {
    eval("var oops = 'Ugh!';");
    console.log(oops);
}

badIdea();   // Ugh!
```

### With

Esta función nos permite tomar como variables locales los elementos de un objeto, por ejemplo:

```
var badIdea = { oops: "Ugh!" };

with (badIdea) {
    console.log(oops);   // Ugh!
}

```


Como puedes ver, si añades alguna propiedad al objeto **badIdea** también vas a poder usarlo como una variable local.


> Este post forma parte de mis notas del libro <a href="https://github.com/getify/You-Dont-Know-JS/blob/2nd-ed/scope-closures/ch1.md" hreflang="en" target="_blank" rel="noopener noreferrer">You Dont Know JS</a>

