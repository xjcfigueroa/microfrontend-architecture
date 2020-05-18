## Arquitectura orientada a micro-componentes.

Este es un ejemplo de una arquitectura orientada a microcomponentes usando un 
ruteador de alto nivel llamado single-api el cual orquesta las diferentes 
aplicaciones (micro-frontends) activandose dependiendo la ruta con la cual 
se haya configurado (ver micro-frontend root-config/src/vue-mf-root-config.js)

Comparando la estructura presentada en este proyecto usando esta tecnologia y con micro-frontends en vue la arquitectura con la que habia realizado el proyecto
tambien con elementos de este tipo de arquitecura utilizaba ya una pagina sobre una pagina web con paginas individuales para cada aplicación,por ejemplo en la pagina de
registro tiene su propia pagina html https://www.24hourfitness.com/registration.html#/

Sabiendo esto podemos comparar cada pagina html ah como cada aplicacion en vuejs 
quedaba aislada comparado con esta arquitectura en la que una sola aplicacion puede tener su propio microfrontend para cada parte (barra de navegacion, calificar perros y ver los perros en tu coleccion) pero tambien poder tener con otra ruta en single-api
o en otra pagina html completamente otra aplicacion independiente a la de la otra ruta o compartir ciertos microfrontends de otras secciones totalmente independiente con single-api se permite tener esta flexibilidad, comparado con el approach en el que se desarrollo la arquitecura con ciertos elmentos de micro-frontend que realize para este cliente se podia comparar al tener una aplicacion completa en un archivo html con cada componente aislado y ya en otro archivo html tener algun componente compartido de la otra aplicacion.

## Estructura del proyecto

El presente proyecto contiene el siguiente orden:

1.- root-config: contiene la aplicacion principal que carga los demas microfrontends contiene la configuracion del ruteador principal dentro de src/vue-mf-root-config.js
aqui se hace referencia a las diferentes rutas en las que los demas microfrontends se cargaran (navbar, rate-dogs, dogs-dashboard).

2.- Styleguide: Contiene componentes compartidos entre los diferentes micro-frontends,
como global.css, component-library/page-header.vue

Esta parte tambien la manejaba en un repo con todo lo comun compartido entre las distintas aplicaciones pero aparte de tenerlo en su propio repo tambien era un modulo de NPM que descargabamos desde el repo privado de npm del cliente.

3.- Navbar: contiene el microfrontend para la barra de navegacion que conforma toda la aplicacion usa el propio router de vue para activar la siguiente ruta y ya cada aplicacion gracias el super router de single-api reacciona creando la interactividad y al mismo tiempo manteniendo aislado cada ambiente.

En este caso cada microfrontend puede tener su propio set de sub componentes que serian componentes solo de presentacion de datos (dumb) y el principal siendo el smart component.

En la arquitectura que desarrolle hace años cada aplicacion y sus componentes estaban ligados uno con otros por ejemplo la parte de mi cuenta tenia sus propios sub compnentes tanto de presentacion (dumb) como componentes smart.

4.- rate-dogs y dogs dashboard siguen la misma estructrua de diseño que la barra de navegacion estos tres micro-frontends son conocidos dentro de single-api como app-parcel ya que son los que conforman la aplicacion en su totalidad aunque son toalmente interoperables e intercabiables dependiendo la ruta deseada en el orquestador superior que es single-api o en el caso de usar otra herramienta como spring con java o algun otro lenguaje del lado del servidor.

5.- Shared dependencies: Solamente tiene un archivo llamada importsmap.json el cual es donde se declaran las dependencias del proyecto como todos los micro-frontends otras dependenicas externas como vue, single-api etc este archivo se usa en el index.ejs en la parte de los imports de System.js para cargar todos los modulos de la aplicacion y para que single-api sepa que cargar a la hora de desplegar una ruta en el navegador.

## Despliegue de micro-frontends

Ya con esta arquitecura es facil ya crearle su pipeline a cada proyecto para realizar un deploy a un servidor ya que cada proyecto independientemente cuenta con una configuracion de webpack que contruye solo el modulo ya listo para ser cargado por single-api cuando una ruta es llamada.

Por ejemplo se puede tener jenkins con los pipelines para desplegar cada micro-frontend a un ambiente de staging o QA para realizar pruebas esto permite 
ya separar responsabildades a cada equipo o desarrollador per micro-frtonetnd y 
avanzar ya cada equipo dado sus tiempos y prioridad sin afectar el release de nuevas funcionalidades de otras partes de la aplicacion como un todo.

### Conclusion:

Siguiendo los lineamientos de esta arquitecura comparado con la que realice con vuejs para desarrollar modulos como de mi cuenta, pagos y visitas a clubs esta puede ser representada directamente usando single-api.
