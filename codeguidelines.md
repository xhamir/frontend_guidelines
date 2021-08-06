# Code guidelines.
Se genera este archivo como una guía lo más específica posible de las reglas de código que debemos seguir y los múltiples casos en los que podemos mejorar para seguir las mejores prácticas. Esta guía se dividirá en dos partes, la primera para nuestro código en Vue y la segunda para nuestros estilos en el proyecto.


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

## Notación de nombres de componentes single-file. Revision-
Los nombres de los archivos de los  componentes single-file deben ser siempre PascalCase o siempre kebab-case.

El autocompletado de los editores de código funciona mejor cuando se utiliza PascalCase, ya que esta es consistente con la forma en que referenciamos componenten en JS(X) y plantillas, dónde sea posible. Sin embargo, nombres de archivos mixtos pueden crear problemas en sistemas de archivos insensibles a las mayúsculas y minúsculas, es por esto que utilizar kebab-case es perfectamente aceptable.

Ejemplo:

    components/  
    |- MyComponent.vue
---

    components/  
    |- my-component.vue

## Nombre de componentes fuertemente acoplados.
Los componentes hijo que están fuertemente acoplados a su padre deben incluir el nombre del componente padre como prefijo.

Si un componente solo tiene sentido en el contexto de un componente padre, dicha relación debe ser evidente en su nombre. Dado que usualmente los editores organizan los archivos alfabéticamente, esto también deja ambos archivos cerca visualmente.

Ejemplo:

    components/  
    |- SearchSidebar.vue  
    |- SearchSidebarNavigation.vue

## Abreviaciones en directivas. Revision-
Las abreviación de directivas (`:`  para  `v-bind`  y  `@`  para  `v-on:`) deben ser utilizadas siempre o nunca.

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

   

# Reglas de codificación en SCSS
Para los estilos por convicción de los desarrolladores del proyecto se utiliza la siguiente metodología:

    scss/  
        |- base/  
        |- components/
        |- layout/
        |- pages/
        |- main.scss
        
   ---
En el archivo main.scss importaremos los archivos creados en las carpetas base, components, layout y pages.

Ejemplo:

    // Abstracts:
    
    // Base:
    @import  "base/utilities";
    
    // Components: TEST COMMENT
    @import  "components/Area_A/initTask";
    @import  "components/Area_A/routeList";
    @import  "components/Home/homeHeader";
    @import  "components/Inventario/detail";
    @import  "components/Inventario/location";
    @import  "components/Inventario/reports";
    @import  "components/Inventario/uploadDBF";
    @import  "components/Receive/notFound";
    @import  "components/Receive/products";
    @import  "components/Route/detailRoute";
    @import  "components/Route/routeAsign";
    @import  "components/Route/routeUserAsignRoute";
    @import  "components/Shared/exportFilesModal";
    @import  "components/Shared/facturas";
    @import  "components/Shared/facturasDetail";
    @import  "components/Shared/header";
    @import  "components/Shared/historial";
    @import  "components/Shared/internetStatus";
    @import  "components/Shared/loading";
    @import  "components/Shared/responseStatus";
    @import  "components/Supervisors/listSupervisor";
    @import  "components/Supervisors/negados";
    @import  "components/Supervisors/objetivo";
    @import  "components/Supervisors/productivity";
    @import  "components/Supervisors/usersControl";
    @import  "components/Supervisors/usersControlDetail";
    @import  "components/Supervisors/verificador";
    @import  "components/Users/CEUser";
    @import  "components/Management/ceManagement";
    @import  "components/AfterSale/claims";
    @import  "components/AfterSale/actions";
    @import  "components/WorkShifts/listEditable";
    
    // Layout:
    @import  "layout/sidebar";
    @import  "layout/footer";
    
    // Pages:
    @import  "pages/areaa";
    @import  "pages/arrangement";
    @import  "pages/classifier";
    @import  "pages/homev2";
    @import  "pages/inventario";
    @import  "pages/login";
    @import  "pages/monitor";
    @import  "pages/planning";
    @import  "pages/printroute";
    @import  "pages/rutas";
    @import  "pages/settings";
    @import  "pages/uploadfile";
---
En la carpeta "base" tenemos las los archivos con estilos globales, los cuales se compartirán en todo el proyecto y componentes existentes.

Ejemplo:

     base/
	     |- _utilities.scss
    	
Los archivos de estilos que codifiquemos deben iniciar con un guion bajo y un nombre representativo. En este caso _utilities.scss.

Contenido:
	

    /* Utilities */
    
    * {
    box-sizing: border-box  !important;
    }
    
    html {
    font-size: 15px;
    }
    
    body {
    background: #1e202a  !important;
    }

---
En la carpeta "components" tenemos las los archivos con estilos específicos para componentes usados en determinadas secciones de nuestro código. Divididos por subcarpetas que describan que sección de nuestro código representan.

Ejemplo:

    components/
    	|-Inventario
	    	|- _detail.scss
    	
 

Contenido:

    .onclicktable {
    padding: 0.75rem;
    }
      
    .detail {
	    margin: 0rem  3.5rem;
	    padding: 2rem  0;
	    &__filter {
		    display: grid;
		    grid-template-columns: 3fr  1fr  1fr;
		    grid-gap: 0.8rem;
		    padding: 1rem;
		    select {
			    border-radius: 5px  !important;
			    padding: 0  0;
			    padding: 0.8rem  0.8rem;
		    }
	    }
    
	    &__header {
		    color: #dbe9ff;
		    padding: 0  1rem;
		    font-size: 1.8rem;
		    display: grid;
		    grid-template-columns: 3fr  2fr  2fr  2fr  2fr  0.5fr;
		    grid-gap: 2rem;
		    &--area {
			    p:first-child {
				    color: #ffffff;
			    }
			    p:last-child {
				    font-size: 1.3rem;
			    }
		    }
    
		    &--inventario {
			    p:first-child {
				    color: #75c124;
			    }
			    p:last-child {
				    font-size: 1.3rem;
			    }
		    }
    
		    &--fisico {
			    p:first-child {
				    color: #ed5824;
			    }
			    p:last-child {
				    font-size: 1.3rem;
			    }
		    }
    
		    &--diferencia {
			    p:first-child {
				    color: #8f1115;
			    }
			    p:last-child {
				    font-size: 1.3rem;
			    }
			}
    
		    &--reportes {
			    border: 1px  solid  gray;
			    p:first-child {
				    text-align: center;
			    }
			    p:last-child {
				    text-align: center;
				    font-size: 1.3rem;
				    margin: 0;
			    }
		    }
    
		    &--download {
			    cursor: pointer;
			    font-size: 3rem;
			    align-self: center;
			    justify-self: center;
			    color: #ed5824;
		    }
	    }
  
	    hr {
		    border-color: #8080802e;
	    }
    }
