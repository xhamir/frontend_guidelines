# Style Guidelines

Se genera este archivo como una guía se busca describir la arquitectura del proyecto con respecto al acomodo de las hojas scss, así como algunas reglas de estilos y mejores practicas.


## Estructura del Proyecto SCSS.
Con el objetivo de mantener una arquitectura consistente en el manejo de los estilos del proyecto y facilitar la organización y reutilización de los estilos, se utilizará un método basado en carpetas el cual se centra en mantener las cosas simples y evidentes.

Por lo tanto, la estructura consiste en tener todas las partes almacenadas en 4 carpetas diferentes (base, components, layout y pages) y un único archivo en el directorio raíz (main.scss) el cual importa todas estas partes para luego compilarlas en una hoja de estilo CSS. Quedando de la siguiente manera:

    scss/
    |- base/
    |  |– _reset.scss       # Reset/normalize
    |  |– _typography.scss  # Reglas tipográficas
    |- components/
    |  |– _buttons.scss     # Botones
    |  |– _carousel.scss    # Carousel
    |- layout/
    |  |– _navigation.scss  # Navegación
    |  |– _grid.scss  # Sistema de retícula
    |  |– _header.scss  # Encabezamiento
    |  |– _footer.scss  # Pie de página
    |  |– _sidebar.scss  # Barra lateral
    |  |– _forms.scss  # Formularios
    |- pages/
    |  |– _home.scss  # Estilos específicos para la página de inicio
    |  |– _contact.scss  # Estilos específicos para la página de contacto
    |  …  # Etc.
    |
    |- main.scss.  # Archivo principal de Sass

En los siguientes apartados, describiremos más a fondo los archivos que contendrán cada una de las carpetas y su relación con la distribución en el sitio o la aplicación.

### CARPETA BASE
La carpeta base/ contiene lo que podríamos llamar la plantilla del proyecto. Allí, puedes encontrar el archivo reset para reiniciar los estilos CSS, algunas reglas tipográficas y probablemente un archivo CSS que define algunos estilos estándares para los elementos HTML más comunes

    _base.scss
    _reset.scss

### CARPETA LAYOUT
La carpeta layout/ contiene todo lo que tiene que ver con la distribución del sitio o la aplicación. Esta carpeta puede contener hojas de estilo para las partes principales del sitio (header, footer, navigation, sidebar…), el sistema de retícula o incluso el estilo CSS para los formularios.

    _grid.scss
    _header.scss
    _footer.scss
    _sidebar.scss
    _forms.scss
    _navigation.scss

### CARPETA COMPONENTES
Para componentes más pequeños, existe la carpeta components/. Mientras layout/ tiene una visión macro (definiendo la estructura global), components/ está mucho más centrado en los widgets. Contiene todo tipo de módulos específicos como por ejemplo, un slider, un loader, un widget, y básicamente todo lo que esté en esa misma línea. Por lo general hay un montón de archivos en components/, ya que todo el sitio o la aplicación debería estar compuesto en su mayoría, de pequeños módulos.

    _media.scss
    _carousel.scss
    _thumbnails.scss

### CARPETA PÁGINAS
Si tienes estilos específicos para cada página (“View”), es mejor ponerlos en una carpeta pages/, dentro de un archivo con el nombre de la página. Por ejemplo, es común tener muchos estilos específicos para la página principal, por lo que existe la necesidad de tener un archivo _home.scss en la carpeta pages/.

    _home.scss
    _contact.scss

### CARPETA ABSTRACTS
La carpeta abstracts/ reúne todas las herramientas y helpers de Sass utilizados en todo el proyecto. Cada variable global, función, mixin y placeholder debería estar en esta carpeta.

La regla de oro para esta carpeta es que no debe generar ni una sola línea de CSS cuando se compila por si sola. Solo hay helpers de Sass.

    _variables.scss
    _mixins.scss
    _functions.scss
    _placeholders.scss


## Style Guidelines – Mejores Prácticas

### Regla 1: Metodología en Cascada
En cada uno de estos archivos para crear una clase para un determinado elemento debemos seguir una metodología de cascada. Donde declararemos el nombre de la clase lo más descriptivo posible.

En el caso de que la sección o componente tenga hijos, los cuales deban heredar alguna característica del padre, pero tener sus propias variantes, estos atributos los diferenciaremos por guiones bajos (__).

Si estos hijos a su vez tienen hijos y se repite la situación, debemos crear sus clases con guiones altos (--). En un caso extremo en que estos últimos también tengan hijos y sigan este patrón, volveremos a usar guiones bajos, y repetiremos la metodología anterior.

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
### Regla 2: Nombre Representativo
Por ejemplo, en la carpeta "base" tenemos los archivos con estilos globales, los cuales se compartirán en todo el proyecto y componentes existentes.

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
### Regla 3: División por sub carpetas que describan la sección que representan.
Tal es el caso de la carpeta "components" en donde tenemos los archivos con estilos específicos para componentes usados en determinadas secciones de nuestro código. Estos a su vez deben estar divididos por sub carpetas que describan que sección de nuestro código representan.

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
### Regla 4: Estilos en forma de elemento, no generales
En la carpeta "layout" agregamos los estilos para las partes que se repiten en todo el proyecto, pero estos deben ser en forma de elementos, no estilos generales. Algunos ejemplos serian el sidebar y un footer.

Ejemplo:

    layout/
    |- _footer.scss
    |- _sidebar.scss

Dichos archivos contendrán los estilos dedicados únicamente a estos elementos que se repiten en todo el proyecto.

Ejemplo:

    .footer-text {
	    //...
    }
---
### Regla 5: Archivos de estilos que correspondan a una respectiva vista ("View")

En la carpeta "pages" colocaremos los archivos de estilos dedicados únicamente a una respectiva "view", componentes específicos de cada vista que vayamos creando.

Ejemplo:

    pages/
    |- _classifier.scss

El contenido de este archivo será clases que apuntan solamente a la vista que "classifier".

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
   
   ---
   ## Sintaxis y Formato
Las guías de estilo de código que fomentan la coherencia no solo previenen esto, sino que también ayudan a la hora de leer y actualizar el código. Por lo tanto, se sugiere el uso de las siguientes mejores practicas para las hojas de estilo.

 1.  **Indentación y tabulación**
	 - Dos (2) espacios en blanco, en lugar de tabulaciones.
	 - Idealmente, líneas de 80 caracteres.
	 - Reglas CSS multilínea correctamente escritas;
	 - Buen uso de los espacios en blanco.

**Ejemplo**:

	```
	// Uso Correcto
	.foo {
	  display: block;
	  overflow: hidden;
	  padding: 0 1em;
	}

	// Uso incorrecto
	.foo {
	    display: block; overflow: hidden;

	    padding: 0 1em;
	}
	```
 **2. Nombrado**

 - Los nombres de los archivos deben usar  `snake_case`.
 - Las clases CSS deben usar el formato `lowercase-hyphenated`  en lugar de  `snake_case`  o  `camelCase`.

**Ejemplo**:
```
// Incorrecto
.class_name {
  color: #fff;
}

// Incorrecto
.className {
  color: #fff;
}

// Correcto
.class-name {
  color: #fff;
}

```
- Deben usarse nombres de clases en lugar de selectores de nombres de etiquetas. Se desaconseja el uso de selectores de nombres de etiquetas porque pueden afectar a elementos no deseados en la jerarquía.

**Ejemplo**:
```
// Incorrecto
ul {
  color: #fff;
}

// Correcto
.class-name {
  color: #fff;
}

// Mejor practica
// Preferir una clase de utility en lugar de agregar estilos existentes

```

- Los nombres de las clases también son preferibles a los ID. Las reglas que usan ID no son reutilizables, ya que solo puede haber un elemento afectado en la página.

**Ejemplo**:

```
// Incorrecto
#my-element {
  padding: 0;
}

// Correcto
.my-element {
  padding: 0;
}

```

3.  Selectores con prefijo js-
- No usar ningún selector con prefijo "js-" para propósitos de estilo. Estos selectores están diseñados para usarse solo con JavaScript para permitir la eliminación o el cambio de nombre sin romper el estilo.

4. Variables
Antes de agregar una nueva variable para un color o un tamaño, garantice:
- No hay uno existente.
- No hay uno similar que podamos usar en su lugar.