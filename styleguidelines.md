# Style guidelines.
Se genera este archivo como una guía lo más específica posible de las reglas de estilos que debemos seguir y los múltiples casos en los que podemos mejorar para seguir las mejores prácticas.

# Reglas de codificación en SCSS.
Para los estilos por convicción de los desarrollados del proyecto se utiliza la siguiente metodología:

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
    
    // Components:
    @import  "components/Area_A/initTask";
    @import  "components/Area_A/routeList";
   
    // Layout:
    @import  "layout/sidebar";
    @import  "layout/footer";
    
    // Pages:
    @import  "pages/areaa";
    @import  "pages/arrangement";
   

En cada uno de estos archivos para crear una clase para un determinado elemento debemos seguir una metodología de cascada. Donde declararemos el nombre la clase lo mas descriptivo posible y en la cual si nuestra sección o componente tiene hijos y estos deben tener heredar características del padre pero tener sus propias variantes de algunos atributos los diferenciaremos por guiones medios. Si estos hijos a su vez tienen hijos y se repite la situación, debemos crear sus clases con guiones altos. En un caso extremo en que estos últimos también tengan hijos y sigan este patrón, volveremos a usar guiones bajos, y repetiremos la metodología anterior.

Ejemplo:

    .home {
	    //...
	    &__box {
		    //..
		    &--minis {
			    //...
			    &__red {
				    //...
				    &--big {
					    //...
					    &__full {
						    //...
					    }
				    }
				}
		    }
	    }
    }

---
En la carpeta "base" tenemos las los archivos con estilos globales, los cuales se compartirán en todo el proyecto y componentes existentes.

Ejemplo:

    base/
	    |- _utilities.scss
    	
Los archivos de estilos que codifiquemos deben iniciar con un guion bajo y un nombre representativo. En este caso _utilities.scss.

Contenido:
	

    /* Utilities */
    
    * {
	    //...
    }
    
    html {
	    //...
    }
    
    body {
	    //...
    }

---
En la carpeta "components" tenemos las los archivos con estilos específicos para componentes usados en determinadas secciones de nuestro código. Divididos por subcarpetas que describan que sección de nuestro código representan.

Ejemplo:

    components/
	    |-Inventario
	    |- _detail.scss
    	
 

Contenido:

    .detail {
	    //...
	    &__filter {
		    //...
		    }
	    }
    
	    &__header {
		    //...
		    &--area {
			    //...
		    }
    
		    &--inventario {
			    //...
		    }
    
		    &--fisico {
			    //...
		    }
    
		    &--diferencia {
			    //...
			}
    
		    &--reportes {
			   //...
		    }
    
		    &--download {
			    //...
		    }
	    }
    }

---
En la carpeta "layout" agregamos los estilos para las partes que se repiten en todo el proyecto pero en forma de elementos no estilos generales. Puede ser un sidebar y un footer por ejemplo.

Ejemplo:

    layout/
	    |- _footer.scss
	    |- _sidebar.scss

Dichos archivos contendran los estilos dedicados unicamente a estos elementos que se repiten en todo el proyecto.


Ejemplo:

    .footer-text {
	    //...
    }

---
En la carpeta "pages" colocaremos los archivos de estilos dedicados únicamente a una respectiva "view", componentes específicos de cada vista que nosotros vayamos creando.

Ejemplo:

    pages/
	    |- _classifier.scss

El contenido de este archivo seran clases que apuntan solamente a la vista que "classifier".

Ejemplo:

    .classifier {
	    //...
	    &__header {
		    //...
	    }
	    &__content {
		    //...
		    &--column:first-child {
			    //...
		    }
	    }
	    &__notFound {
		    //...
	    }
    }
