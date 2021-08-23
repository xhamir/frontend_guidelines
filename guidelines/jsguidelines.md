# Guidelines de codificación de JavaScript

Este es un conjunto de reglas y convenciones de codificación para su uso en la programación de JavaScript. Está inspirado en las convenciones de código del documento de Sun para el lenguaje de programación Java. Este mismo esta modificado para ser utilizado en en lenguaje de programación Javascript.

El valor a largo plazo del software para una organización es directamente proporcional a la calidad del código base. Durante su vida útil, un programa será manejado por muchos pares de manos y ojos. Si un programa es capaz de comunicar claramente su estructura y características, es menos probable que se rompa cuando se modifique en un futuro no muy lejano.

Las convenciones de código pueden ayudar a reducir la fragilidad de los programas.

Todo nuestro código JavaScript se envía directamente al público. Siempre debe ser de calidad de publicación.

## Archivos de JavaScript

El código JavaScript no debe estar incrustado en archivos HTML a menos que el código sea específico para una sola sesión. El código en HTML aumenta significativamente el peso de la página sin posibilidad de mitigación mediante el almacenamiento en caché y la compresión.

`<script src=filename.js>`  Las etiquetas de tipo "script" deben colocarse lo más tarde posible dentro de la etiqueta "body". Esto reduce los efectos de las demoras impuestas por las secuencias de comandos dentro de la etiqueta script en otros componentes de la página. 

## Indentation

La sangría utilizada debe ser de cuatro espacios. Se debe evitar el uso de "tabs" porque todavía no existe un estándar para la ubicación de los "tabs". El uso de espacios puede producir un mayor tamaño en el archivo, pero el tamaño no es significativo en las redes locales.

## Longitud de línea

Evite las líneas de más de 80 caracteres. Cuando un enunciado no cabe en una sola línea, puede ser necesario romperlo. Coloque el salto después de un operador, idealmente después de una coma. Una pausa después de un operador reduce la probabilidad de que un error de copiar y pegar quede enmascarado por la inserción de punto y coma. La siguiente línea debe tener una sangría de 8 espacios.

## Comentarios

Sea generoso con los comentarios. Es útil dejar información que será leída más adelante por personas (posiblemente usted mismo) que necesitarán comprender lo que ha hecho. Los comentarios deben estar bien escritos y ser claros, al igual que el código que están anotando. Se puede agradecer una pizca de humor ocasional.

Es importante que los comentarios se mantengan actualizados. Los comentarios erróneos pueden hacer que los programas sean aún más difíciles de leer y comprender.

Haga comentarios significativos. Concéntrese en lo que no es visible de inmediato. No pierdas el tiempo del lector con cosas como:

    i = 0; // Set i to zero.

Generalmente usé comentarios de línea. Guarde los comentarios de bloque para la documentación formal.

## Declaración de variables

Todas las variables deben ser declaradas antes de usarse. JavaScript no requiere esto, pero hacerlo hace que el programa sea más fácil de leer y facilita la detección de variables no declaradas que pueden convertirse en globales implícitas. Nunca se deben utilizar variables globales implícitas.

Las declaraciones var o let deben ser las primeras declaraciones en el cuerpo de la función.

  
Se prefiere que cada variable tenga su propia línea y comentario. Deben aparecer en orden alfabético.

    let currentEntry, // currently selected table entry
        level = 0,    // indentation level
        size;         // size of table

Crear arrays usando sintaxis de literal en lugar de new Array

    Recomendado: var a = [x1, x2, x3];
    No usar: var a = new Array(x1, x2, x3);

Crear objetos usando sintaxis de literal en lugar de new Object

    Recomendado: var a = { };
    No usar: var a = new Object ();

## Declaración de Funciones

Todas las funciones deben declararse antes de que se utilicen.

No debe haber espacio entre el nombre de una función y el paréntesis izquierdo de su lista de parámetros. Debe haber un espacio entre el paréntesis derecho y la llave izquierda que comienza el cuerpo de la declaración. El cuerpo en sí tiene una sangría de cuatro espacios. La llave derecha está alineada con la línea que contiene el comienzo de la declaración de la función.

    function outer(c, d) {
        let e = c * d;
    
        function inner(a, b) {
            return (e * a) + b;
        }
    
        return inner(0, 1);
    }

Esta convención funciona bien con JavaScript porque en JavaScript, las funciones y los objetos literales se pueden colocar en cualquier lugar donde se permita una expresión. Proporciona la mejor legibilidad con funciones en línea y estructuras complejas.

    function getElementsByClassName(className) {
        let results = [];
        walkTheDOM(document.body, function (node) {
            let a;                  // array of class names
            let c = node.className; // the node's classname
            let i;                  // loop counter
    
           // If the node has a class name, then split it into a list of simple names.
           // If any of them match the requested name, then append the node to the set of results.
            if (c) {
                a = c.split(' ');
                for (i = 0; i < a.length; i += 1) {
                    if (a[i] === className) {
                        results.push(node);
                        break;
                    }
                }
            }
        });
        return results;
    }

Si una función literal es anónima, debe haber un espacio entre la palabra función y el paréntesis izquierdo. Si se omite el espacio, puede parecer que el nombre de la función es función, lo cual es una lectura incorrecta.

    div.onclick = function (e) {
        return false;
    };
    
    that = {
        method: function () {
            return this.datum;
        },
        datum: 0
    };


Cuando una función debe invocarse inmediatamente, toda la expresión de invocación debe incluirse entre los padres para que quede claro que el valor que se produce es el resultado de la función y no la función en sí.

    var collection = (function () {
        var keys = [], values = [];
    
        return {
            get: function (key) {
                var at = keys.indexOf(key);
                if (at >= 0) {
                    return values[at];
                }
            },
            set: function (key, value) {
                var at = keys.indexOf(key);
                if (at < 0) {
                    at = keys.length;
                }
                keys[at] = key;
                values[at] = value;
            },
            remove: function (key) {
                var at = keys.indexOf(key);
                if (at >= 0) {
                    keys.splice(at, 1);
                    values.splice(at, 1);
                }
            }
        };
    }());

## Nombres de variables y funciones

Los nombres, evitar el uso de caracteres internacionales porque es posible que no se lean bien o no se entiendan en todas partes. No use $ (signo de dólar) o \ (barra invertida) en los nombres de variables.

No utilice _ (barra inferior) como primer carácter de un nombre. A veces se utiliza para indicar privacidad, pero en realidad no proporciona privacidad. Si la privacidad es importante, use los formularios que brindan los miembros privados. Evite las convenciones que demuestren una falta de competencia.
La mayoría de las variables y funciones deben comenzar con una letra minúscula.

Las constantes deben ser escritas en mayúsculas.

## Declaraciones

### Declaraciones Simples

Cada línea debe contener como máximo una declaración. Poner un ; (punto y coma) al final de cada declaración simple. Tenga en cuenta que una instrucción de asignación que asigna una función literal o un objeto literal sigue siendo una instrucción de asignación y debe terminar con un punto y coma.

JavaScript permite que cualquier expresión se utilice como declaración. Esto puede enmascarar algunos errores, particularmente en presencia de inserción de punto y coma. Las únicas expresiones que deben usarse como declaraciones son asignaciones e invocaciones.

### Declaraciones compuestas

Las declaraciones compuestas son declaraciones que contienen listas de declaraciones encerradas entre {} (llaves).

Las declaraciones adjuntas deben tener una sangría de cuatro espacios más. La {(llave izquierda) debe estar al final de la línea que comienza la declaración compuesta. La} (llave derecha) debe comenzar una línea y tener una sangría para alinearse con el comienzo de la línea que contiene la {(llave izquierda) correspondiente. Deben usarse llaves alrededor de todas las declaraciones, incluso declaraciones individuales, cuando son parte de una estructura de control, como una declaración if o for. Esto hace que sea más fácil agregar declaraciones sin introducir errores accidentalmente. 

### Declaración del return 

Una declaración de retorno con un valor no debe usar () (paréntesis) alrededor del valor. La expresión del valor de retorno debe comenzar en la misma línea que la palabra clave de retorno para evitar la inserción de punto y coma.

### Declaración if 

La clase de declaraciones if debe tener la siguiente forma:

    if (condition) {
        statements
    }
    
    if (condition) {
        statements
    } else {
        statements
    }
    
    if (condition) {
        statements
    } else if (condition) {
        statements
    } else {
        statements
    }

### Declaración for 

Una clase de declaraciones for debe tener la siguiente forma:

    for (initialization; condition; update) {
        statements
    }
    
    for (variable in object) {
        if (filter) {
            statements
        } 
    }

La primera forma debe usarse con matrices y con bucles de un número predeterminado de iteraciones.

La segunda forma debe usarse con objetos. Tenga en cuenta que los miembros que se agreguen al prototipo del objeto se incluirán en la enumeración. Es aconsejable programar a la defensiva utilizando el método hasOwnProperty para distinguir los verdaderos miembros del objeto:

    for (variable in object) {
        if (object.hasOwnProperty(variable)) {
            statements
        } 
    }

### Declaración while 

Una declaración while debe tener la siguiente forma:

    while (condition) {
        statements
    }

### Declaración do while

Una declaración do while debe tener la siguiente forma:

    do {
        statements
    } while (condition);

A diferencia de las otras sentencias compuestas, la sentencia do siempre termina con ; (punto y coma).

### Declaración switch 

Una declaración switch debe tener la siguiente forma:

    switch (expression) {
    case expression:
        statements
    default:
        statements
    }


Cada caso está alineado con el interruptor. Esto evita la indentación excesiva.

Cada grupo de declaraciones (excepto las predeterminadas) debe terminar con break, return o throw. No te caigas.

### Declaración try 

Una declaración try debe tener la siguiente forma:

    try {
        statements
    } catch (variable) {
        statements
    }

    try {
        statements
    } catch (variable) {
        statements
    } finally {
        statements
    }

### Declaración continue

Evite el uso de la declaración de continue. Tiende a oscurecer el flujo de control de la función.

## Espacios en blanco

Las líneas en blanco mejoran la legibilidad al establecer secciones de código que están relacionadas lógicamente.

Los espacios en blanco deben usarse en las siguientes circunstancias:

Una palabra clave seguida de ((paréntesis izquierdo) debe estar separada por un espacio.

while (verdadero) {

No se debe usar un espacio en blanco entre el valor de una función y su ((paréntesis izquierdo). Esto ayuda a distinguir entre palabras clave e invocaciones de funciones. Todos los operadores binarios excepto. (Punto) y ((paréntesis izquierdo) y [(paréntesis izquierdo) deben estar separados de sus operandos por un espacio. Ningún espacio debe separar un operador unario y su operando excepto cuando el operador es una palabra como typeof. Cada ; (punto y coma) en la parte de control de una instrucción for debe ir seguido de un espacio. Los espacios en blanco deben seguir cada , (coma).

## {} y []

Utilice matrices cuando los nombres de los miembros sean números enteros secuenciales. Utilice objetos cuando los nombres de los miembros sean cadenas o nombres arbitrarios.

## Operador , (comma) 

Evite el uso del operador de coma, excepto para un uso muy disciplinado en la parte de control de las declaraciones for. (Esto no se aplica al separador de comas, que se usa en literales de objeto, literales de matriz, declaraciones var y listas de parámetros).

## Block Scope

En JavaScript los bloques no tienen alcance. Solo las funciones tienen alcance. No utilice bloques excepto según lo requieran las declaraciones compuestas.

## Expresiones de asignación

Evite hacer asignaciones en la parte de condición de las declaraciones if y while.

if (a = b) { }

Declaración correcta:

if (a == b) { }

## Operadores === and !== 

Casi siempre es mejor utilizar los operadores === y! ==. Los operadores == y! = Escriben coerción. En particular, no use == para comparar con valores falsos.



