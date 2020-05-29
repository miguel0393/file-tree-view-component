# Taller Bimestral - Desarrollo de software basado en componentes (En progreso)

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

## Listado de requisitos funcionales

- The component must be developed as a Vue.js 2.0 app.

- The component shall be a treeview frontend component that could be embedded in a
webapp. Its data shall be saved in JSON format at the browser’s local storage.

- At the beginning, the treeview component shall have a button. Once the user clicks on
it, he shall be able to type a name. Once it is done, that will be the tree’s name and its root node.

- The root node will have the following operations:
    - Delete tree (via right click), which will delete the whole tree.
    - Add subfolder (via right click), which will ask for a name and will append the corresponding subfolder to the root node.
    - Expand/collapse (via double click), which will expand/collapse the whole tree.

- Every subfolder will have the following operations:
    - Delete subfolder (via right click), which will delete the folder and its content.
    - Add file (via right click), which will ask for a name and will append the corresponding file to the subfolder.
    - Expand/collapse (via double click), which will expand/collapse the corresponding subfolder.

- Every files will have the following operations:
    - Delete file (via right click), which will delete the file and its content.
    - Modify file (via right click), which will ask for the content (text) of the file and will store it.
    - Show file (via double click), which will show the content of the file (text).