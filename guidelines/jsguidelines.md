# Javascript guidelines.
Se genera este archivo como una guía lo más específica posible de las reglas de código que debemos seguir y los múltiples casos en los que podemos mejorar para seguir las mejores prácticas.

# Reglas de codificación en Javascript.
Los programadores JavaScript suelen atenerse a unas reglas de estilo a la hora de escribir código. No son de obligado cumplimiento. Tan sólo son recomendaciones que buscan que el código sea más fácil de leer y entender y siga unos estándares.

Declarar siempre las variables usando var. No hacerlo dificulta interpretar en qué ámbito se encuentra la variable y puede ocasionar que una variable esté en ámbito global indebidamente.

Ejemplo:

    var nodosDiv;

Usa siempre puntos y coma para delimitar el final de una instrucción o línea. Cuando una función funciona como una expresión, debe delimitarse con punto y coma final. En cambio, en las declaraciones de funciones no se usa punto y coma final.

Ejemplo:

    var mivar1 = function() {

      return true;

    }; // Aquí incluir punto y coma final

    function miFuncion1() {
    
      return true;

    } // Aquí no incluimos punto y coma final

