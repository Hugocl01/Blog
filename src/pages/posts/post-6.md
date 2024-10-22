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