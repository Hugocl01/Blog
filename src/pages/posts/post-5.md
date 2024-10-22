---
layout: ../../layouts/MarkdownPostLayout.astro
title: Fundamentos de JavaScript
author: Hugo Cayón Laso
description: "Una guía básica sobre los elementos clave de JavaScript: variables, operadores, estructuras de control y más."
image:
    url: "https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png"
    alt: "Logo de JavaScript"
pubDate: 2024-10-20
readingTime: 9 min
tags: ["JavaScript", "Frontend", "Desarrollo web"]
---

## Introducción

JavaScript es un lenguaje de programación orientado a objetos y multiplataforma, utilizado principalmente para hacer páginas web interactivas. En este post, abordaremos los conceptos clave para entender cómo funciona, desde la declaración de variables hasta los operadores y estructuras de control.

## Elementos básicos de JavaScript

### Etiqueta `<script>`

El código JavaScript se puede incluir directamente en un documento HTML mediante la etiqueta `<script>`. También puedes enlazar archivos externos con la propiedad `src`. Para asegurar que el archivo se cargue tras el HTML, es recomendable usar el atributo `defer`.

```html
<script src="app.js" defer></script>
```

### Comentarios de código

Los comentarios son útiles para documentar el código y pueden ser de una sola línea `//` o múltiples líneas `/* */`.

```js
// Esto es un comentario de una línea
/*
  Esto es un comentario de múltiples líneas
*/
```

### Declaración de variables

En JavaScript, puedes declarar variables usando `let`, `const` o `var`. let se usa para variables locales que pueden cambiar su valor, mientras que `const` define constantes que no pueden ser reasignadas.

```js
let nombre = 'Hugo';
const PI = 3.14;
```

### Tipado dinámico

JavaScript es un lenguaje de **tipado débil**, lo que significa que una variable puede cambiar su tipo durante la ejecución del programa.

```js
let dato = 'Texto';
dato = 42;  // Ahora es un número
```

### Tipos de datos

JavaScript admite tipos de datos primitivos como:

* **String** ("Hola", 'Texto')
* **Number** (42, 3.14)
* **Boolean** (true, false)
* **null** (valor vacío intencional)
* **undefined** (valor no asignado)

Y tipos no primitivos como **Object** y **Array**.
### Operadores

#### Operadores aritméticos

Permiten realizar operaciones matemáticas como suma (+), resta (-), multiplicación (*), división (/), y módulo (%).

```js
let suma = 5 + 3; // 8
let potencia = 2 ** 3; // 8 (2 elevado a 3)
```

#### Operadores de comparación

Compara dos valores, por ejemplo:

* &gt; (mayor que)
* &lt; (menor que)
* &gt;= (mayor o igual)
* &lt;= (menor o igual)
* == (igual sin comparar tipos de datos)
* != (diferente sin comparar tipos de datos)
* === (estrictamente igual)
* !== (estrictamente diferente)

```js
console.log(5 > 3); // true
console.log(5 === '5'); // false
```

#### Operadores lógicos

Se usan para combinar condiciones:

* AND (&&)
* OR (||)
* NOT (!)

```js
console.log(true && false); // false
console.log(!true); // false
```

#### Valores "falsy"

JavaScript considera ciertos valores como "falsy" cuando se evalúan en un contexto booleano, como 0, "", null, undefined, NaN y false.

Lista de valores "falsy":

* null
* undefined
* false
* NaN
* 0, 0.0, 0x0
* -0, -0.0, -0x0
* 0n. NOTA: no existe -0n.
* "", '', `` Cadena vacía.
* document.all

Todos los valores que no son "falsy" son "truthy".

### Estructuras de control

#### Condicional `if`

Evalúa una condición y ejecuta el bloque de código correspondiente si es verdadera.

```js
if (edad > 18) {
  console.log("Es mayor de edad");
} else {
  console.log("Es menor de edad");
}
```

#### Bucle `for`

Se usa para iterar sobre un bloque de código un número determinado de veces.

```js
for (let i = 0; i < 5; i++) {
  console.log(i); // 0, 1, 2, 3, 4
}
```

#### Bucle `for...of`

Este bucle itera sobre los elementos de un array u objeto iterable.

```js
let frutas = ['Manzana', 'Banana', 'Naranja'];
for (let fruta of frutas) {
  console.log(fruta);
}
```

#### Bucle `for...in`

Este bucle itera sobre las propiedades de un objeto.

```js
let persona = { nombre: "Hugo", edad: 30 };
for (let propiedad in persona) {
  console.log(propiedad);  // nombre, edad
}
```

#### Bucle `while`

Ejecuta el código mientras la condición sea verdadera.

```js
let i = 0;
while (i < 5) {
  console.log(i);
  i++;
}
```

#### Bucle `do...while`

El bucle `do...while` garantiza que el bloque de código se ejecuta al menos una vez antes de evaluar la condición.

```js
let i = 0;
do {
  console.log(i);
  i++;
} while (i < 5);
```

### Instrucciones `continue` y `break`

#### Instrucción `break`

La instrucción `break` se utiliza para salir de un bucle de forma anticipada, es decir, cuando se cumple una condición determinada dentro del bucle, el flujo de ejecución salta fuera del mismo.

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break;  // El bucle se detiene cuando i es igual a 5
  }
  console.log(i);  // Imprime los números del 0 al 4
}
```

#### Instrucción `continue`

La instrucción continue se utiliza para saltar la iteración actual del bucle y pasar a la siguiente, sin detener completamente el bucle.

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    continue;  // Salta la iteración cuando i es igual a 5
  }
  console.log(i);  // Imprime todos los números excepto el 5
}
```

### Arrays y Objetos

#### Arrays

Un array es una lista de elementos que pueden ser accedidos mediante su índice.

```js
let frutas = ['Manzana', 'Banana'];
console.log(frutas[0]); // Manzana
```

#### Objetos (JSON)

Un objeto es una colección de pares clave-valor.

```js
let persona = { nombre: "Hugo", edad: 30 };
console.log(persona.nombre); // Hugo
```

### Funciones

Las funciones en JavaScript son bloques de código reutilizables que permiten ejecutar una tarea específica. Se pueden definir de varias formas según las necesidades del desarrollador.

#### Funciones con nombre

Son las funciones tradicionales, definidas con la palabra clave `function` y un nombre que las identifica.

```js
function saludo(nombre) {
  return `Hola, ${nombre}`;
}

console.log(saludo("Ana")); // "Hola, Ana"
```

Estas funciones se pueden invocar en cualquier parte del código después de su declaración.

#### Parámetro variable `(...rest)`

JavaScript permite definir funciones que aceptan un número indeterminado de argumentos utilizando el parámetro rest `(...)`.

```js
function sumar(...numeros) {
  return numeros.reduce((acumulado, num) => acumulado + num, 0);
}

console.log(sumar(1, 2, 3, 4)); // 10
```

Aquí, `...numeros` recoge todos los argumentos pasados y los convierte en un array que luego se utiliza dentro de la función.
Funciones anónimas

#### Funciones anónimas

Son funciones que no tienen nombre y generalmente se asignan a variables o se pasan como argumentos a otras funciones.

```js
const multiplicar = function (a, b) {
  return a * b;
};

console.log(multiplicar(3, 4)); // 12
```

Las funciones anónimas suelen ser usadas en callbacks.

#### Arrow functions

Las arrow functions son una sintaxis más concisa para escribir funciones. Además, no crean su propio contexto `this`, lo que las hace útiles en ciertas situaciones.

```js
const restar = (a, b) => a - b;
console.log(restar(10, 5)); // 5
```

Si la función tiene un único parámetro, se pueden omitir los paréntesis, y si el cuerpo de la función tiene solo una expresión, se puede omitir el return y las llaves.

#### Closures

Un closure se forma cuando una función interna tiene acceso a las variables de su función externa, incluso después de que la función externa haya terminado su ejecución.

```js
function crearContador() {
  let contador = 0;
  return function () {
    contador++;
    return contador;
  };
}

const incrementar = crearContador();
console.log(incrementar()); // 1
console.log(incrementar()); // 2
```

En este ejemplo, la función interna sigue accediendo a la variable contador aunque la función `crearContador` ya haya terminado de ejecutarse.

#### Funciones auto invocadas (IIFE)

Las funciones IIFE (Immediately Invoked Function Expression) son funciones que se invocan inmediatamente después de ser definidas.

```js
(function () {
  console.log("Esta función se ejecuta automáticamente");
})();
```

Se utiliza para ejecutar código sin contaminar el espacio de nombres global, manteniendo las variables dentro del ámbito de la función.

### Modo Estricto: `'use strict'`

A estas alturas, ya hemos visto que JavaScript tiene muchas particularidades que pueden dar lugar a errores. Para limitar estos problemas, se añadió el **modo estricto** en ES5, que fomenta el uso de código más seguro y moderno en JavaScript.

#### ¿Cómo habilitar el modo estricto?

Puedes habilitar el modo estricto mediante la instrucción `'use strict'`. Esta instrucción admite dos ámbitos de uso:

- **A nivel de script**: Debe ser la primera instrucción del script y se aplica a todo el código del mismo.
- **A nivel de función**: Debe ser la primera instrucción de la función y se aplica únicamente a esa función.

> **IMPORTANTE**: Si la instrucción no es la primera en el ámbito correspondiente, no se activará el modo estricto.

#### Principales características del modo estricto

El modo estricto activa un conjunto de reglas que proporcionan un entorno más seguro, lo que implica lo siguiente:

- **No puedes usar variables sin declararlas**: Todas las variables deben ser declaradas con `var`, `let` o `const`.
- **No puedes usar la instrucción `delete`**: La eliminación de propiedades de objetos se restringe.
- **No puedes mezclar distintas notaciones matemáticas**: Se evita la confusión entre octales y decimales.
- **No puedes usar palabras reservadas como nombres de variable**: Algunas palabras están reservadas por el lenguaje y no se pueden utilizar como identificadores.
- **No puedes definir dos parámetros con el mismo nombre**: Por ejemplo, `fn(p1, p1)` generará un error.
- **En Programación Orientada a Objetos (POO)**: No puedes escribir en propiedades de solo lectura ni leer en propiedades de solo escritura (getters y setters).
- **La función `eval()`** no puede definir variables por seguridad.
- **El objeto `this`** en funciones ahora es `undefined`: Normalmente, hace referencia al objeto `window`, pero en el modo estricto, `this` es `undefined`.

Con el modo estricto, puedes escribir código más robusto y evitar errores comunes en JavaScript, lo que mejora la mantenibilidad y la legibilidad de tus proyectos.

## Conclusión

¡Y así llegamos al final! Hemos recorrido juntos muchos de los conceptos esenciales de JavaScript, desde las bases como la declaración de variables y operadores, hasta funciones avanzadas como las arrow functions, closures, y las auto-invocadas IIFE. Además, exploramos cómo manejar estructuras de control, arrays, objetos, y más, para que puedas darle vida a tus proyectos.

JavaScript es un lenguaje versátil y poderoso, pero como todo en la programación, la práctica es lo que realmente te ayudará a dominarlo. No te preocupes si al principio parece mucho, todos hemos pasado por ahí. Lo importante es que sigas experimentando, aprendiendo y, sobre todo, divirtiéndote mientras lo haces.

Espero que este post te haya servido como un buen punto de partida o de repaso. Si tienes preguntas o comentarios, no dudes en compartirlos. ¡Gracias por leer y sigue creando cosas geniales con JavaScript!

¡Nos vemos en el próximo post👋!