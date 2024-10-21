---
layout: ../../layouts/MarkdownPostLayout.astro
title: Fundamentos de JavaScript
author: Hugo Cayón Laso
description: "Una guía básica sobre los elementos clave de JavaScript: variables, operadores, estructuras de control y más."
image:
    url: "https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png"
    alt: "Logo de JavaScript"
pubDate: 2024-10-20
readingTime: 7 min
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

Todo los valores que no son "falsy" son "truthy".

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

## Instrucciones `continue` y `break`

### Instrucción `break`

La instrucción `break` se utiliza para salir de un bucle de forma anticipada, es decir, cuando se cumple una condición determinada dentro del bucle, el flujo de ejecución salta fuera del mismo.

```js
for (let i = 0; i < 10; i++) {
  if (i === 5) {
    break;  // El bucle se detiene cuando i es igual a 5
  }
  console.log(i);  // Imprime los números del 0 al 4
}
```

### Instrucción `continue`

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

#### Funciones con nombre

Las funciones son bloques de código que realizan una tarea específica. Se pueden definir con la palabra clave function.

```js
function saludar() {
  console.log("Hola!");
}
saludar(); // Llama a la función
```

#### Arrow functions

Es una sintaxis más concisa para definir funciones.

```js
const sumar = (a, b) => a + b;
console.log(sumar(2, 3)); // 5
```
