---
title: "¿Cómo utilizar el Método substring en JavaScript?"
subtitle: "Aprende a utilizar el método substring en JavaScript para extraer partes específicas de un string Descubre cómo manipular eficientemente strings en tus proyectos web."
tags: ["javascript","string concatenation",]
date: "2020-10-19T16:36:30+00:00"
authors: []
status: "published"

---


El método de [Javascript](https://4geeks.com/es/lesson/que-es-javascript-aprende-a-programar-en-javascript) `substring()` es utilizado para devolver únicamente una parte de la cadena original partiendo desde el índice inicial establecido y continua hasta el final de la cadena. Opcionalmente se puede especificar el índice final como parámetro.

```js
let myString = "4geeks Academy";

console.log(myString.substring(7)); //Consola: Academy

console.log(myString.substring(0, 6)); // Consola: 4geeks

```

Usualmente cuando manejamos variables que contienen texto en Javascript, tenemos la necesidad de aplicarle distintas transformaciones o métodos hasta lograr el resultado que esperamos. `substring()` es uno de los métodos más utilizados debido a su flexibilidad al momento de manipular o extraer porciones específicas del texto sin necesidad de modificar la variable original. En este artículo aprenderemos la forma correcta para invocar el método y los detalles que debemos tomar en cuenta para obtener el resultado que necesitamos.

## Utilizando el método de Javascript Substring

El método `substring()` es inherente de la clase String, por lo que para poder invocarlo debemos hacerlo necesariamente desde un objeto de tipo String.

### Sintaxis de Javascript substring()

```js
myString.substring(indiceInicial)
ó
myString.substring(indiceInicial, indiceFinal)

```

#### Parámetros:

`indiceInicial`: Es la posición inicial de la porción que se desea extraer.

`indiceFinal`: Es la posición final de la porción que se desea extraer. Este parámetro es opcional.

```js
let myString = "4geeks Academy"; 

let indiceInicial = 0
let indiceFinal = 6
  
let result = myString.substring(indiceInicial, indiceFinal); 
  
console.log(result); // Consola: 4geeks
```

Algo importante a tomar en cuenta al momento de utilizar este método es que **el parámetro indiceFinal es **"exclusivo"** lo cual significa que debemos utilizar el índice del último caracter que queremos incluir en la substring **más 1**.

En el siguiente ejemplo podremos notar como esto puede afectar el resultado, si tomamos en cuenta que los índices de la string `"4geeks"` llegan hasta el 5, donde el caracter `"4"` se ubica en el índice 0 y el último caracter `"s"` se ubica en el índice 5 quedando de la siguiente forma:

```js
let myString = "4geeks"; 

// Entonces si utilizamos 5 como indiceFinal obtendremos:
console.log(myString.substring(1, 5)); // Consola: geek

// Mientras que si le sumamos: 5 + 1 el resultado será:
console.log(myString.substring(1, 6)); // Consola: geeks
```

## Utilizando `substring()` de Javascript con la propiedad `length`

La propiedad `length`, que tienen todos los objetos de tipo String, puede ser de mucha utilidad cuando estamos aplicando el método `substring()` ya que no necesitamos saber cual es la cantidad de posiciones entre el inicio de la cadena y la posición donde queremos iniciar la extracción, sino únicamente la cantidad de caracteres que queremos extraer al final de la cadena.

Por ejemplo, si únicamente nos interesan los últimos 6 caracteres :

```js
let firstString = "Academia 4geeks";
let secondString = "Es una excelente academia 4geeks";
let thirdString = "Ven a aprender en 4geeks";

let indiceInicial = 6;

console.log(firstString.substring(firstString.length - indiceInicial)); // Consola: 4geeks

console.log(secondString.substring(secondString.length - indiceInicial)); // Consola: 4geeks

console.log(thirdString.substring(thirdString.length - indiceInicial)); // Consola: 4geeks
```
  
### Otros ejemplos  

```js
let myString = "4geeks Academy";

// Si queremos obtener unicamente el primer caracter
let first_result = myString.substring(0, 1); 
console.log(first_result); // Consola: 4

// En el siguiente código extraemos los últimos 3 caracteres de la cadena
let second_result = myString.substring(myString.length - 3);
console.log(second_result); // Consola: emy

// En el siguiente código extraemos el caracter en la posición myString.length -8
let third_result = myString.substring(myString.length - 9, myString.length - 8)
console.log(third_result) // Consola: s

// En el siguiente código extraemos el caracter en el medio de la cadena
let middleIndex = myString.length / 2
let forth_result = myString.substring(middleIndex, middleIndex + 1)
console.log(forth_result) // Consola: A
```
  
  
## Conclusión 

El método `substring()` puede ser de mucha utilidad cuando manejamos cadenas de caracteres, por ello es muy importante saber utilizarlo tomando en cuenta las distintas opciones de parametrización que tiene disponibles. Si te interesa conocer más sobre  Javascript puedes revisar este artículo sobre [aprender a programar en Javascript](https://4geeks.com/es/lesson/que-es-javascript-aprende-a-programar-en-javascript), aquí puedes encontrar información muy interesante y aprende este lenguaje desde cero con ejemplos de código, videotutoriales y muchos más recursos que te serán muy útiles para practicar y conocer más sobre el lenguaje de programación Javascript. Puedes leer más sobre este y otros temas en el Blog de [4Geeks](https://4geeks.com/).
