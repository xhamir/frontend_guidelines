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

## Uso de Eslint.

Eslint es una herramienta que analiza nuestro código y encuentra problemas con nuestro código; como errores de sintaxis, código que no encaja con alguna convención definida que tengamos presente y malas practicas en general dentro del proyecto.

Vue hace uso de esta herramienta como parte de la extensión vue/cli-plugin-eslintla cual utiliza la versión actualmente 6.7.2 o mayores al dia que este leyendo este documento, esto del lado del framework.

EsLint del lado del dresarrollador

Al momento de desarrollar el proyecto RECI los desarrolladores nos encontramos usando VSCode como IDE con Vue para desarrollar la aplicación, sin embargo solo se estaba haciendo uso de algunas extensiones de VsCode para apoyarnos en el dia a dia para detectar errores comunes de sintaxis y potenciales malas practicas dentro de este, pero no se cuenta con ninguna relación que garantiza este proceso del lado de los despliegues del proyecto a través de la infraestructura con la que contamos.

A continuación se presentan las herramientas que utilizamos del lado de desarrollo y configuraciones que irán de la mano para asi despues describir como se integrara esta herramienta del lado de nuestro proceso de CI/CD.

Extensiones de desarrollo

La siguiente lista es una lista recomendada de extensiones para garantizar la mejor experiencia de desarrollo posible dentro de cualquier proyecto que utilice Vue:

EsLint ^2.1.4 → linter que utilizamos dentro del proyecto para la detección de problema en el código.

Path intellisense 2.2.1 → ayuda para auto completado de rutas de archivos.

Vetur 0.26.1 → Herramienta que cuenta con varias funcionalidades para trabajar con vue como highlight de la sintaxis, revisión de código y auto completado de sintaxis-

Vue 2 Snippets 0.12.1 → Encuentras casi todos los snippets de código de la API de vue

Configuraciones para eslint

Actualmente se añadió el siguiente archivo .eslintrc.json con la siguiente configuración:

    {
	    "env": {
		    "browser": true,
		    "es2020": true
	    },
	    "extends": [
		    "eslint:recommended",
		    "plugin:vue/essential"
	    ],
	    "parserOptions": {
		    "ecmaVersion": 11,
		    "sourceType": "module"
	    },
	    "plugins": [
		    "vue"
	    ],
	    "globals": {
		    "process": "readonly"
	    },
	    "rules": {
		    "no-mixed-spaces-and-tabs": "off",
		    "no-empty-function": "error",
		    "no-eval": "error",
		    "no-extend-native": "error"
	    }
    }

A continuación una breve explicación de cada uno de los elementos de la configuración:

env → ambientes en los cuales el código sera validado, como RECI es una aplicación web se valida en los ambientes de navegadores y bajo el estándar ECMASCRIPT 2020.

extends: Incluye configuraciones recomendadas ya configuradas para trabajar en tu proyecto en este caso añadimos las recomendadas de eslint mas las recomendadas por vue, estas configuraciones son paquetes separados de NPM.

parserOptions → Configuraciones especificas del parseador de slint para validar el código.

globals: Variables globales dentro de la aplicación las cuales se agregan en esta lista para ser ignoradas a la hora de validar el código también se puede utilizar el comentario /* globals var1, var2 */

rules → Aquí se pueden alterar reglas ya definidas dentro de la parte de extends o agregar nuevas o modificar el nivel de importancia de una regla ya predefinida dentro de eslint:recommended por ejemplo

También se agrego el archivo .eslintignore para ignorar algún archivo especifico (como la carpeta de unit tests) como nota ademas de agregar alguna carpeta que se desee ignorar dentro de este archivo también debe especificarse el path de la carpeta que contiene los archivos de nuestro proyecto esto se puede visualizar dentro de los comandos de linting que tenemos en el proyecto los cuales apuntan a la carpeta src.

## Comandos del proyecto para correr el linter.

Dentro de package.json se cuenta con dos comandos las cuales nos sirven para hacer lint del cogido el comando “lint“ es el que viene nativo dentro del proyecto y se agrego el comando “eslint“ para dado algún caso especifico tener mas flexibilidad con el debugging de eslint.

"lint": "vue-cli-service lint src",

"eslint": "eslint --ext .js,.vue src -c .eslintrc.json",

Ambos comandos apuntan como lo mencione a la carpeta src la cual contiene los archivos del proyecto.

## Archivo de configuraciones de VSCode.

El siguiente es el archivo de configuraciones para el editor es recomendado como complemento de lo ya mencionado en este documento:

	    {
	    "vetur.format.defaultFormatter.html": "js-beautify-html",
	    "javascript.format.insertSpaceBeforeFunctionParenthesis": true,
	    "eslint.validate": [
		    "vue",
		    "html",
		    "javascript"
	    ],
	    "eslint.codeAction.showDocumentation": {
		    "enable": true
	    },
	    "editor.codeActionsOnSave": {
		    "source.fixAll": true
	    },
	    "editor.rulers": [100,120],
	    "editor.detectIndentation": true,
	    "editor.tabSize": 2
    }
