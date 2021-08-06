# Code guidelines.
Se genera este archivo como una guía lo más específica posible de las reglas de código que debemos seguir y los múltiples casos en los que podemos mejorar para seguir las mejores prácticas. 

# Reglas de codificación en Vue.

Estas reglas ayudan a prevenir errores. Pueden existir excepciones, pero deben ser muy raras y sólo las deben realizar aquellas personas con conocimientos de JavaScript y Vue.

## Nombres de componentes de varias palabras.
Los nombres de los componentes siempre deben ser de varias palabras, a excepción de los componentes raíz de la “App”. Esto evita conflictos con elementos HTML existentes y futuros, ya que todos los elementos HTML son una sola palabra.

Ejemplo:

    Vue.component('todo-item', {  
	    // ...  
    })

---

    export default {  
	    name: 'TodoItem',  
	    // ...  
    }


## Componente data.
El componente  `data`  debe ser una función.

Al usar la propiedad  `data`  en un componente (es decir, en cualquier lugar excepto en`new Vue`), el valor debe ser una función que devuelve un objeto.

Ejemplo:

    Vue.component('some-comp', {  
	    data: function () {  
		    return {  
			    foo: 'bar'  
		    }  
	    }  
    })

---

    // En un archivo .vue  
    
    export default {  
	    data () {  
		    return {  
			    foo: 'bar' 
		    }  
	    }  
    }

---

    // Está bien usar un objeto directamente  
    // en una instancia raíz de Vue,  
    // ya que solo existirá esa única instancia.  
    
    new Vue({  
	    data: {  
		    foo: 'bar'  
	    }  
    })

## Definiciones props.
Las definiciones de Props deben ser lo mas detalladas posible.

En el código “commiteado”, las definiciones de props siempre deben ser lo más detalladas posible, especificando al menos su(s) tipo(s).

Ejemplo:


    props: {  
    	status: String  
    }
---

    // Mucho mejor!  
    
    props: {  
	     status: {  
		     type: String,  
		     required: true,  
		     validator: function (value) {  
			     return [  
				     'syncing',  
				     'synced',  
				     'version-conflict',  
				     'error'  
			     ].indexOf(value) !== -1  
		     }  
	     }  
     }


## Key y v-for. Revision-
Siempre use  `key`  con  `v-for`.

`key`  con  `v-for`  es un requisito en componentes, para mantener el estado del componente interno en el subárbol. Sin embargo, incluso para los elementos, es una buena práctica mantener un comportamiento predecible, como  constancia del objeto en las animaciones. Todo esto cuando se tenga un id en el objeto a iterar.

Ejemplo:

    <ul>
	    <li 
	    v-for="todo in todos" 
	    :key="todo.id"
	    >
		    {{ todo.text }}  
	    </li>  
    </ul>

## Evitar v-if con v-for.
Nunca use  `v-if`  en el mismo elemento que  `v-for`.

Hay dos casos comunes en los que esto puede ser tentador:

-   Para filtrar elementos en una lista (por ejemplo,  `v-for="user in users" v-if="user.isActive"`). En estos casos, reemplace  `users`  con una nueva propiedad calculada que devuelva su lista filtrada (por ejemplo  `activeUsers`).
    
-   Para evitar renderizar una lista si debe estar oculta (por ejemplo,  `v-for="user in users" v-if="shouldShowUsers"`). En estos casos, mueva el  `v-if`  a un elemento contenedor (por ejemplo,`ul`,  `ol`).

Ejemplo:

    <ul>  
	     <li  
	     v-for="user in activeUsers"  
	     :key="user.id"  
	     >  
		     {{ user.name }}  
	     <li>  
    </ul>
---

    <ul 
    v-if="shouldShowUsers"
    >  
	     <li  
	     v-for="user in users"  
	     :key="user.id"  
	     >  
		     {{ user.name }}  
	     <li>  
    </ul>

## Cada componente debe ser un archivo.
Siempre que un compilador pueda concatenar archivos, cada componente debería estar en su propio archivo.

Esto lo ayudará a usted a encontrar de una manera más rápida un componente cuando precise editarlo o verificar como se utiliza.

Ejemplo:

    components/  
    |- TodoList.vue  
    |- TodoItem.vue

## Notación de nombres de componentes single-file.
Los nombres de los archivos de los  componentes single-file deben ser siempre PascalCase.

El autocompletado de los editores de código funciona mejor cuando se utiliza PascalCase, ya que esta es consistente con la forma en que referenciamos componenten en JS(X) y plantillas, dónde sea posible.

Ejemplo:

    components/  
    |- MyComponent.vue

## Nombre de componentes fuertemente acoplados.
Los componentes hijo que están fuertemente acoplados a su padre deben incluir el nombre del componente padre como prefijo.

Si un componente solo tiene sentido en el contexto de un componente padre, dicha relación debe ser evidente en su nombre. Dado que usualmente los editores organizan los archivos alfabéticamente, esto también deja ambos archivos cerca visualmente.

Ejemplo:

    components/  
    |- SearchSidebar.vue  
    |- SearchSidebarNavigation.vue

## Abreviaciones en directivas.
Las abreviación de directivas (`:`  para  `v-bind`  y  `@`  para  `v-on:`) deben ser utilizadas siempre.

Ejemplo incorrecto:

    <input  
     v-bind:value="newTodoText"  
     :placeholder="newTodoInstructions"  
    >
    
   --- 
      <input  
     v-on:input="onInput"  
     @focus="onFocus"  
    >
---
Ejemplo correcto:

    <input  
     :value="newTodoText"  
     :placeholder="newTodoInstructions"  
    >
---

    <input  
     @input="onInput"  
     @focus="onFocus"  
    >

## Añadir lineas vacías al código.
Añadir una línea vacía entre propiedades que se extienden en múltiples líneas, particularmente si las opciones no entrar en la pantalla sin  _scrollear_.

Cuando un componente comienza a sentirse apretado o difícil de leer, añadir espacios entre propiedades que se extienden en múltiples líneas puede mejorar la legibilidad. En algunos editores, como Vim, opciones de formateo como esta pueden facilitar la navegación con el teclado.

Ejemplo:

    props: {  
	    value: {  
		    type: String,  
		    required: true  
	    },  
      
	    focused: {  
		    type: Boolean,  
		    default: false  
	    },  
      
	     label: String,  
	     icon: String  
    },  
      
    computed: {  
	    formattedValue: function () {  
		    // ...  
	    },  
      
	    inputClasses: function () {  
		    // ...  
	    }  
    }