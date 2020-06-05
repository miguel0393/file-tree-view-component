# Taller Bimestral - Desarrollo de software basado en componentes

Desarrollado por:

* Miguel Bolívar Osorio  (mbolivaro@eafit.edu.co)
* Oscar Soto (osotoduq@eafit.edu.co)
* Pablo Gutierrez Lopez (pgutier6@eafit.edu.co)

Para la materia "Desarrollo de software basado en componentes"

Universidad EAFIT - 2020


## Requisitos del sistema

* Vue.js 2.6
* Node.js


## Instalación

* Instalar Node.js en primera instancia y comprobar su disponibilidad usando

```bash
$ node -v
```
* Instalar las dependencias del proyecto 

```bash
$ cd file-tree-view-component
$ npm install
```

## Ejecutar la aplicación

```bash
$ npm run serve
```

Luego de hecho el build la aplicación quedará accesible en la siguiente URL con la funcionalidad de live reload activada

```bash
http://localhost:8080/ 

```


## Introduccion

**Nombre del componente**: Componente de vista de árbol de archivos (File Tree Visualizer)

**Objetivo**: El objetivo es desarrollar un componente de software reutilizable, que pueda almacenar datos en carpetas y subcarpetas.

**Descripción**: Este componente permite hacer una navegación en una estructura tipo árbol de carpetas y archivos permitiendo realizar operaciones de manipulación sobre estos elementos y manteniendo una copia actualizada de la estructura en el almacenamiento LocalStorage del navegador web.

**Audiencia del componente**: El componente de navegación en árbol está orientado a desarrolladores que deseen incorporar el componente tal cual se entrega a sus proyectos particulares. Sin embargo y a pesar de no tener parametrización e inicialización personalizada, el componente también puede ser usado por otro grupo de desarrolladores que deseen usarlo como parte de un sistema mayor donde se haga composición de componentes.



## Especificación de requisitos


La construcción del componente está regida por los siguientes requisitos funcionales

#### requisito ID FR1.01.01
El componente debe desarrollarse como una aplicación Vue.js 2.0.

#### Requisito ID FR1.02.01
El componente será un componente frontend de vista de árbol que podría integrarse en una aplicación web. Sus datos se guardarán en formato JSON en el almacenamiento local del navegador.

#### Requisito ID FR1.03.01
Al principio, el componente de vista de árbol tendrá un botón. Una vez que el usuario haga clic en él, podrá escribir un nombre. Una vez hecho, ese será el nombre del árbol y su nodo raíz.

#### Requisito ID FR1.04.01
El nodo raíz tendrá las siguientes operaciones:
- Eliminar árbol (haciendo clic derecho), que eliminará todo el árbol.
- Agregue una subcarpeta (haciendo clic con el botón derecho), que solicitará un nombre y agregará la subcarpeta correspondiente al nodo raíz.
- Expandir / contraer (mediante doble clic), que expandirá / contraerá todo el árbol.


#### Requisito ID FR1.05.01
Cada subcarpeta tendrá las siguientes operaciones:
- Eliminar subcarpeta (haciendo clic con el botón derecho), que eliminará la carpeta y su contenido.
- Agregue el archivo (haciendo clic con el botón derecho), que solicitará un nombre y agregará el archivo correspondiente a la subcarpeta.
- Expandir / contraer (mediante doble clic), que expandirá / contraerá la subcarpeta correspondiente.

#### Requisito ID FR1.06.01
Todos los archivos tendrán las siguientes operaciones:
- Eliminar archivo (mediante clic derecho), que eliminará el archivo y su contenido.
- Modifique el archivo (haciendo clic con el botón derecho), que solicitará el contenido (texto) del archivo y lo almacenará.
- Mostrar archivo (mediante doble clic), que mostrará el contenido del archivo (texto).


## Dependencias

Para hacer modificaciones al código fuente del componente se necesita contar con las siguientes dependencias de desarrollo.

- Vue 2.6.11
- Node.js 10.x

## Estructura visual del componente

El componente de visualización de árbol de archivos se compone de dos secciones cada una ocupando el 50% del ancho de la pantalla.
La zona izquierda muestra la estructura del árbol y su contenido mientras que la zona derecha está destinada a mostrar el contenido de texto dentro de los archivos.

![Estructura general del componente](/../../media/images/tree-general.png?raw=true "Estructura general del componente")

## Referencia de código

El código del componente está organizado en archivos y carpetas siguiendo el estándar de proyectos en Vue.js y el esqueleto creado por la utilidad de línea de comandos `vue-cli`:

![Estructura de codigo](/../../media/images/project-structure.png?raw=true "Estructura de codigo")

La carpeta src es la carpeta raíz del código del componente:

- **Assets**: La carpeta assets contiene recursos gráficos y estilos.
- **Images**: La carpeta images contiene las todas las imágenes utilizadas en el componente.
- **Styles**: En la carpeta styles se encuentran los archivos CSS para los estilos del componente. Siguiendo la mayor independencia de componentes posible, se maneja un archivo de estilos para cada componente Vue.
- **Components**: La carpeta components contiene los componentes Vue. Cada componente se compone de: una parte HTML con anotaciones Vue para maquetar su contenido, una parte de código JavaScript para el comportamiento, y un enlace a la hoja de estilos correspondiente.
- El archivo App.vue es el punto de entrada de la aplicación donde se hace uso del componente.

## Estructura interna del componente

El componente de visualización de árbol de archivos es el resultado de la colaboración de otros componentes internos que proveen funcionalidades específicas.

El punto de entrada se encuentra en el componente `FileTreeVisualizer` quien actúa como un orquestador manejando el estado global de la visualización del árbol, recibiendo eventos de los componentes colaboradores y actuando de acuerdo a ellos. Estos otros componentes son:

- `FileTreeBrowser`: Muestra en pantalla cada uno de los nodos del árbol y controla el nivel de anidamiento entre ellos tanto en la parte lógica como visual.
- `FileContent`: Muestra el contenido de un archivo el cual es recibido como prop 
- `ContextMenu`: Provee la funcionalidad de mostrar menús contextuales y despachar eventos de acuerdo a la opción elegida para posterior procesamiento.
- `ModalDialog`: Muestra una ventana tipo modal para el ingreso de datos por parte del usuario para las diferentes acciones disponibles.

Estos componentes están escritos nativamente en Vue.js y no hacen uso de dependencias externas.

## Inicialización del componente en un proyecto Vue


Para usar el componente en un nuevo proyecto de Vue es necesario importar el componente `FileTreeVisualizer` e incluirlo dentro del template de la aplicación donde se vaya a usar por medio de la etiqueta `<FileTreeVisualizer>`.

#### props

- `showFolderOpt`: Prop de tipo booleano. Si es `false` los folders del nodo raíz no tendrán la opción de crear subfolders dentro de ellos. Para activar esta función se debe pasar el prop en `true`. Por defecto el prop está inicializado en `false`.

```javascript
<FileTreeVisualizer :showFolderOpt="false"/>
```

A continuación un ejemplo en código de esta inicialización en un archivo `App.vue`

```javascript
<template>
  <div id="app">
    <h1>File Tree-View Component</h1>
    <FileTreeVisualizer :showFolderOpt="false"/>
  </div>
    
</template>

<script>
import FileTreeVisualizer from "./components/FileTreeVisualizer.vue";

export default {
  name: "App",
  props: { },
  components: {
    FileTreeVisualizer
  }
};
</script>

<style></style>
```

## Inicialización del componente en un proyecto HTML/JS convencional

Vue provee una forma de construir y simplificar el componente en la menor cantidad de archivos posible por medio del comando `npm run build`.
Al realizar la construcción del componente se obtiene una estructura como esta en la carpeta `/dist`

![Carpeta dist](/../../media/images/dist-structure.png?raw=true "Carpeta dist")

Para incluir el componente dentro de un archivo HTML convencional se sugiere inicializar los encabezados y el cuerpo del HTML de la siguiente manera

```html
<!DOCTYPE html>
<html lang=en>

<head>
    <meta charset=utf-8>
    <meta http-equiv=X-UA-Compatible content="IE=edge">
    <meta name=viewport content="width=device-width,initial-scale=1">
    <link rel=icon href=/favicon.ico> <title>file-tree-viewer</title>
    <link href=/css/styles.css rel=preload as=style>
    <link href=/js/app.js rel=preload as=script>
    <link href=/js/vendors.js rel=preload as=script>
    <link href=/css/styles.css rel=stylesheet>
</head>

<body><noscript><strong>JS not enabled or supported</strong></noscript>
    <div id=app></div>
    <script src=/js/vendors.js> </script> 
    <script src=/js/app.js> </script> 
</body> 
</html>
```

**Cuándo usar**: El Componente de vista de árbol de archivos está diseñado para visualizar una estructura de directorios y archivos. La estructura de archivos se crea desde cero dentro del mismo componente y se guarda en formato JSON en el LocalStorage del navegador. Por lo tanto, el componente puede acoplarse a distintas aplicaciones web que necesiten un visor de archivos que permita a los usuarios ver, crear y editar directorios y archivos.

**Cuándo no usar**: Cuando se requiera tener persistencia de la estructura mostrada en el árbol más allá de la que ofrece LocalStorage. Esto incluye almacenamiento en un archivo externo, base de datos o servicio remoto en cloud.
Tampoco se recomienda su uso cuando se desee almacenar archivos de otro tipo diferentes a archivos de texto plano ya que no está implementada una funcionalidad de carga y almacenamiento de archivos.

## Referencia de diseño

**Estilo visual**: El componente presenta un estilo visual simple, para mantener el componente tan independiente de otros componentes (como un framework CSS) como sea posible. 

Para representar las carpetas y archivos en el componente, se cuenta con tres iconos distintos:

Carpeta cerrada

![Carperta cerrada](/../../media/images/folder.png?raw=true "Carpeta cerrada")

Carpeta abierta

![Carperta abierta](/../../media/images/openfolder.png?raw=true "Carpeta abierta")

Archivo

![Archivo](/../../media/images/file.png?raw=true "Archivo")

Los botones usados a dentro del componente tienen un estilo simple, sin ninguna convención de colores en particular:

![Boton](/../../media/images/tree-button.png?raw=true  "Boton")

Cada uno de los nodos del árbol tiene un estado visual hover para identificar más fácilmente en cuál se aplicarán los eventos de mouse:

![Hover Arbol](/../../media/gifs/tree-hover.gif?raw=true "Hover Arbol")


### Especificación CSS

 
A continuación, se especifican los archivos CSS y los selectores mas importantes usados en cada uno de ellos:
 

- `file-tree-visualizer.css`
    - `#app` y `#tree-container`: Con estos selectores se agregan algunos estilos generales para todo el componente file-tree-visualizer, como el tipo de fuente y la alineación del texto.
    - `#tree`: Con este selector se controlan algunos estilos especificos para el panel file-tree-browser.


- `file-tree-browser.css`
    - `.node`: Con esta clase se controlan los estilos para cada elemento (nodo) del árbol, es decir, carpetas y archivos.
    - `.node-name`: Controla los estilos para los nombres de archivos.
    - `.node-name.folder`: Controla los estilos para los nombres de carpetas.
    - `.elements`: Este selector controla el div que contiene los iconos y nombre del nodo. 
    - `.collapsed`, `.expanded`, `.file-node`, `.node-name`: con estas clases se controlan los estilos para los íconos de archivos y carpetas.
    - `#create-tree-btn`: este selector maneja los estilos para el botón de crear árbol.

 
- `modal.css`
    - `.modal`: Con esta clase se controlan los estilos generales de la ventana modal.
    - `.modal input[type="text"]`: Con este selector se controlan los estilos del campo de texto.
    - `.modal textarea`: Con este selector se controlan los estilos del textarea, para el contenido del archivo.
    - `.modal button`: Con este selector se controlan los estilos de los botones de la ventana modal.


- `file-content.css`
    - `#file-content` y `.content`: Estos selectores controlam los estilos generales del panel de visualización del contenido de archivos.


- `contetx-menu.css`
    - `.custom-cm`: Con esta clase se controlan los estilos generales de la ventana para el menú contextual (menú click derecho).
    - `.custom-cm__item`: Con esta clase se controlan los estilos para cada elemento del menú.


## Operaciones disponibles en el árbol

Todas las operaciones descritas a continuación alteran la estructura almacenada en LocalStorage una vez son ejecutadas.

### Inicialización del árbol

Al iniciar el componente por primera vez se mostrará el botón "Create tree" el cual permitirá inicializar el árbol con un nombre para su raíz.

![Inicializar árbol](/../../media/gifs/create-tree.gif?raw=true "Inicializar árbol")

Al ingresar y confirmar el nombre del árbol se creará en LocalStorage del navegador una entrada con nombre `treeStructure` y un valor inicial en formato string 

```javascript
{"name":"nombre_ingresado","children":[]}
```

### Operaciones click derecho en la raíz del árbol

Sobre la raíz del árbol por medio de click derecho están disponibles las siguientes operaciones

![Operaciones de raíz](/../../media/images/tree-operations.png?raw=true "Operaciones de raíz")

- **Add subfolder**: Agrega una carpeta ligada directamente a la raíz del árbol con el nombre especificado.

![Agregar subfolder a raíz](/../../media/gifs/root-add-folder.gif?raw=true "Agregar subfolder a raíz")

- **Add File**: Agrega un archivo vacío a la raíz del árbol. Se abre una ventana modal para ingresar el nombre del archivo.

![Agregar archivo a raíz](/../../media/gifs/root-add-file.gif?raw=true "Agregar archivo a raíz")

- **Delete tree**: Borrar la estructura completa del árbol dejando en LocalStorage un string representando una estructura JSON vacía.

![Borrar árbol](/../../media/gifs/root-delete.gif?raw=true "Borrar árbol")

### Operaciones click derecho sobre una carpeta

![Operaciones de folder](/../../media/images/folder-operations.png?raw=true "Operaciones de folder")

- **Add subfolder**: Agrega una nueva carpeta ligada directamente a la carpeta existente. Esta operación solo está disponible cuando el prop `showFolderOpt` se ha pasado con valor `true`

- **Add file**: Agrega un nuevo archivo vacío con el nombre especificado en la ventana modal.

![Agregar archivo a folder](/../../media/gifs/folder-create-file.gif?raw=true "Agregar archivo a folder")

- **Delete subfolder**: Borra el folder y su contenido interno. Tenga muy en cuenta que todos los contenidos internos, incluyendo archivos, son eliminados también.

![Borrar folder](/../../media/gifs/folder-delete.gif?raw=true "Borrar folder")

### Operaciones click derecho sobre un archivo

![Operaciones de archivo](/../../media/images/file-operations.png?raw=true "Operaciones de archivo")

- **Modify file**: Permite modificar el contenido del archivo ingresando texto por medio de la ventana modal.

![Modificar archivo](/../../media/gifs/file-modify.gif?raw=true "Modificar archivo")

- **Delete file**: Borra el archivo y su contenido interno.

![Borrar archivo](/../../media/gifs/file-delete.gif?raw=true "Borrar archivo")

**Nota: Para ocultar el menú haga click en cualquier zona del contenedor del árbol**

### Operaciones de doble click sobre el árbol

- **Doble click sobre la raíz del árbol**: Expande el árbol en su totalidad mostrando todo su contenido interno. Un nuevo doble click sobre la raíz del árbol lo contrae en su totalidad.

- **Doble click sobre una carpeta**: Expande el contenido de la carpeta en particular mostrando su contenido interno.

- **Doble click sobre un archivo**: Muestra el contenido del archivo en la zona derecha de la pantalla

