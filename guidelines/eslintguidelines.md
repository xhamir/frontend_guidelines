# Eslint guidelines.
Se genera este archivo como una guía lo más específica posible de las reglas de [] que debemos seguir y los múltiples casos en los que podemos mejorar para seguir las mejores prácticas.

# Reglas de codificación en ESlint.

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