---
layout: ../../layouts/MarkdownPostLayout.astro
title: Fundamentos de Arrays y Objetos en JavaScript
author: Hugo Cayón Laso
description: "Una guía sobre arrays y objetos en JavaScript, explorando sus propiedades, métodos y ejemplos prácticos."
image:
    url: "https://upload.wikimedia.org/wikipedia/commons/6/6a/JavaScript-logo.png"
    alt: "Logo de JavaScript"
pubDate: 2024-10-22
readingTime: 8 min
tags: ["JavaScript", "Frontend", "Desarrollo web"]
---

## Introducción

Despues de empezar con los conceptos basico de JavaScript en el [post anterior](post-5), ahora exploraremos dos de sus estructuras de datos más importantes: **arrays** y **objetos**. Aprenderemos cómo funcionan, sus propiedades y métodos, y cómo se pueden utilizar para crear aplicaciones dinámicas y efectivas.

## Arrays en JavaScript

Un **array** es una lista de elementos que se pueden acceder mediante un índice. Los arrays son dinámicos y pueden contener cualquier tipo de datos, incluyendo otros arrays y objetos.

### Creación de Arrays

Puedes crear un array de varias maneras:

```js
let frutas = ['Manzana', 'Banana', 'Naranja']; // Array de frutas
let numeros = new Array(1, 2, 3, 4, 5); // Usando el constructor
```

### Arrays Multidimensionales

En JavaScript, los arrays multidimensionales se crean utilizando arrays dentro de otros arrays. Esto simula múltiples dimensiones, donde cada elemento del array principal puede ser otro array. Uno de los casos más comunes es el uso de un array para representar una matriz, como una tabla de 2D con filas y columnas.

```js
let matriz = [
  [1, 2, 3],   // Fila 1
  [4, 5, 6],   // Fila 2
  [7, 8, 9]    // Fila 3
];
```

### Copia de arrays

Hacer una copia de un array puede no ser tan simple como parece. Si no tienes cuidado, podrías acabar creando una referencia al array original en lugar de una copia. 

#### Copia superficial (shallow copy)

Una copia superficial copia los elementos de un array a un nuevo array. Sin embargo, si los elementos son objetos o arrays, solo se copiará la referencia de estos, no los objetos en sí.

Algunos métodos para hacer una copia superficial de un array son:
Usando el método `slice()`

```js
let original = [1, 2, 3];
let copia = original.slice();
console.log(copia);  // [1, 2, 3]
``` 

Este método devuelve una copia del array original sin modificarlo.

Usando el operador de propagación (`...`)

El operador de propagación (`spread`) también permite crear una copia superficial de un array de forma sencilla.

```js
let original = [1, 2, 3];
let copia = [...original];
console.log(copia);  // [1, 2, 3]
```

#### Copia profunda (deep copy)

En el caso de arrays que contienen objetos o arrays anidados, una copia superficial no es suficiente. Necesitamos una copia profunda (deep copy) que duplique también los elementos internos. Existen varias formas de lograr esto, aunque JavaScript no tiene una solución integrada para copias profundas de forma nativa.

#### Usando JSON

Una forma sencilla de hacer una copia profunda es convertir el array a una cadena JSON y luego volverlo a convertir en un array. Este método funciona bien para arrays de objetos simples, pero no es ideal si el array contiene funciones o referencias a otros objetos especiales.

```js
let original = [[1, 2], [3, 4]];
let copiaProfunda = JSON.parse(JSON.stringify(original));

console.log(copiaProfunda);  // [[1, 2], [3, 4]]
``` 

En este caso, se ha creado una nueva copia profunda del array, sin compartir referencias con el original.
Diferencias entre Copia Superficial y Copia Profunda

Es importante entender la diferencia entre una copia superficial y una profunda. Si modificamos un array superficialmente copiado que contiene objetos o arrays anidados, los cambios también afectarán al array original porque ambos comparten la referencia a esos objetos internos.

```js
let original = [[1, 2], [3, 4]];
let copiaSuperficial = [...original];

// Modificamos la copia superficial
copiaSuperficial[0][0] = 99;

console.log(original[0][0]);  // 99 (también afecta al original)
```

En este caso, cambiar un valor en la copia superficial también cambia el array original, porque ambos comparten la referencia al subarray [1, 2].

### Recorrer Arrays

Podemos utilizar varios operadores o métodos. A continuación se detallan las opciones disponibles:

#### Operadores
   
1. for

* Este bucle nos permite iterar mediante un índice.
* Es útil cuando necesitamos controlar el índice o interrumpir el bucle.

```js
const array = [1, 2, 3, 4, 5];

for (let i = 0; i < array.length; i++) {
    console.log(array[i]);  // Imprime cada elemento del array
}
```

2. for..of

* Devuelve cada valor de la colección.
* Es más legible y simple que for cuando no se necesita el índice.

```js
const array = [1, 2, 3, 4, 5];

for (const value of array) {
    console.log(value);  // Imprime cada valor del array
}
```

3. for..in

* Está pensado para recorrer propiedades. En el caso de los arrays, devuelve el índice en lugar del valor.
* Es menos común para recorrer arrays, ya que está más orientado a objetos.

```js
const array = [1, 2, 3, 4, 5];

for (const index in array) {
    console.log(index);  // Imprime los índices (0, 1, 2, 3, 4)
    console.log(array[index]);  // Imprime los valores usando los índices
}
```

#### Métodos

Los métodos son funciones asociadas a los arrays que nos permiten recorrer o transformar elementos sin la necesidad de usar un bucle explícito. A continuación se presentan dos métodos comunes:

1. .forEach()

* Es similar a for..of. Recorre el array aplicando una función a cada elemento.
* No permite interrumpir el recorrido con break o continue, pero sí podemos usar return para evitar ejecutar más código dentro de la función.

```js
const array = [1, 2, 3, 4, 5];

array.forEach((value) => {
    if (value === 3) return;  // Similar a un 'continue'
    console.log(value);  // Imprime 1, 2, 4, 5
});
```

2. .map()

* Devuelve un nuevo array en el que cada elemento ha sido transformado por la función que pasamos como argumento.
* No modifica el array original, sino que crea una copia con los elementos transformados.

```js
const array = [1, 2, 3, 4, 5];

const newArray = array.map((value) => {
    return value * 2;  // Multiplica cada elemento por 2
});

console.log(newArray);  // Imprime [2, 4, 6, 8, 10]
```

### Diferencias importantes entre operadores y métodos:

* Interrupción de ejecución:
  * Con operadores como for, se puede utilizar break o continue para interrumpir o saltar iteraciones.
  * Los métodos como .forEach() y .map() no permiten break o continue, pero se puede usar return para evitar más acciones en una iteración específica.

* Mutabilidad:
  * Los métodos como .map() crean una nueva copia del array, mientras que for, for..of, y .forEach() operan sobre el array original (aunque .forEach() no lo modifica directamente, sino que solo aplica operaciones).

* Legibilidad:
  * Los métodos pueden ser más legibles y expresivos cuando se realizan operaciones comunes en cada elemento.
  * Sin embargo, los operadores ofrecen más flexibilidad para controlar el flujo de iteración.