---
type: doc
layout: reference
category: Basics
title: Coding Conventions
---

# Convenciones de Codificación

Esta página contiene el estilo de codificación actual para el lenguaje Kotlin.

## Estilos de nombramiento
En caso de duda, por defecto use las convenciones de codificación en Java, tales como:

* Usar camelCase para nombres. (Y evitar el subrayado en los nombres)
* Los tipos comienzan con mayuscula.
* Métodos y propiedades comienzan con minuscula.
* usar 4 espacios para la identación.
* Las funciones públicas deben tener documentación tal como aparezce en Kotlin Doc.

## Llaves

Hay un espacio antes de la llave donde la llave separa el tipo y el supertipo y no hay espacio donde la llave separa la instancia y el tipo:

``` kotlin
interface Foo<out T : Any> : Bar {
    fun foo(a: Int): T
}
```

## Lambdas

En las expresiones lambda, se deben usar espacios alrededor de las llaves, así como alrededor de la flecha que separa los parámetros del cuerpo. Siempre que sea posible, un lambda debe pasar fuera de los paréntesis.

``` kotlin
list.filter { it > 10 }.map { element -> element * 2 }
```

En lambdas que son cortos y no anidados, se recomienda utilizar la convención `it` en lugar de declarar el parámetro
explícitamente. En lambdas anidados con parámetros, los parámetros siempre deben declararse explícitamente.

## Formato de encabezado de clase

Las clases con pocos argumentos pueden escribirse en una sola línea:

```kotlin 
class Person(id: Int, name: String)
```

Las clases con encabezados más largos deben formatearse de modo que cada argumento del constructor primario esté en una línea separada con indentación. Además, el paréntesis de cierre debe estar en una nueva línea. Si utilizamos la herencia, la llamada del constructor de superclase o la lista de interfaces implementadas Debe ubicarse en la misma línea que el paréntesis:

```kotlin 
class Person(
    id: Int, 
    name: String,
    surname: String
) : Human(id, name) {
    // ...
}
```

Para las interfaces múltiples, la llamada del constructor de la superclase debe ser localizada primero y entonces cada interfaz debe estar situada en una línea diferente:

```kotlin 
class Person(
    id: Int, 
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker {
    // ...
}
```

Los parámetros del constructor pueden utilizar el guión regular o el guión de continuación (doble el guión regular).

## Unit

Si una función devuelve Unit, el tipo de retorno debe omitirse:

``` kotlin
fun foo() { // ": Unit" is omitted here

}
```

## Funciones vs Propiedades

En algunos casos, las funciones sin argumentos pueden ser intercambiables con propiedades de sólo lectura.
Aunque la semántica es similar, hay algunas convenciones estilísticas sobre cuándo preferir uno a otro.

Preferir una propiedad sobre una función cuando el algoritmo subyacente:

* No arroja ninguna excepción
* Tiene una complejidad de `O(1)`
* El costo del calculo es bajo (o es calculado en la primera ejecución)
* Devuelve el mismo resultado sobre invocaciones
