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

![Estructura visual del componente](../media/images/tree-general.png?raw=true)

![Alt text](/../../media/images/tree-general.png?raw=true "Optional Title")

![Demo Animation](../assets/demo.gif?raw=true)



