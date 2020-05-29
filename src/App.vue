<template>
  
  <div id="app" @click="onClick">
    <h1>Files Tree-View Component</h1>
    
    <TreeBrowser class="tree" :node="root" @onClick="nodeWasClicked" @onRightClick="showContextMenu" @treeUpdated="treeWasUpdated" />

    <FileContent :content="content" />

    <ContextMenu :xPosition="contextMenuXPosition" :yPosition="contextMenuYPosition" :visible="contextMenuIsVisible"
      @onClick="showModalDialog"
    />
    <ModalDialog :visible="modalDialogIsVisible" :title="modalTitle" :description="modalDescription" @onClick="hideModalDialog"/>
  </div>
</template>

<script>
import TreeBrowser from "./components/TreeBrowser.vue";
import FileContent from "./components/FileContent.vue";
import ContextMenu from "./components/ContextMenu.vue";
import ModalDialog from "./components/ModalDialog.vue";

export default {
  name: "App",
  props: {
    content: {
      type: String,
      default: "CONTENIDO DEL ARCHIVO AQUÍ"
    },
    contextMenuXPosition: Number,
    contextMenuYPosition: Number,
    contextMenuIsVisible: {
      type: Boolean,
      default: false
    },
    modalDialogIsVisible: {
      type: Boolean,
      default: true
    },
    modalTitle: {
      type: String,
      default: "Cambiar Nombre"
    },
    modalDescription: {
      type: String,
      default: "Ingrese el nombre del nodo raíz"
    }
  },
  data() {
    return {
      // root: {
      //   name: "/",
      //   children: [
      //     {
      //       name: "createTreeData1.js",
      //       content: "Contenido de prueba 1",
      //     },
      //     {
      //       name: "createTreeData2.js",
      //       content: "Contenido de prueba 2",
      //     },
      //   ],
      // },
      root: {},
    };
  },
  created(){
     if (localStorage.treeStructure) {
      this.root = JSON.parse(localStorage.treeStructure);
    }
  },
  methods: {
    nodeWasClicked(node) {
      this.content = node.content;
    },
    treeWasUpdated(){
      localStorage.treeStructure = JSON.stringify(this.root);
    },
    showContextMenu(e) {
      this.contextMenuIsVisible = true;
      this.contextMenuXPosition = e.x;
      this.contextMenuYPosition = e.y;
    },
    showModalDialog(tilte, description) {
      this.contextMenuIsVisible = false;
      this.modalDialogIsVisible = true;
      this.modalTitle = tilte;
      this.modalDescription = description;
    },
    hideModalDialog() {
      this.modalDialogIsVisible = false;
    },
    onClick() {
      this.contextMenuIsVisible = false;
    }
  },
  components: {
    TreeBrowser,
    FileContent,
    ContextMenu,
    ModalDialog
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

body {
  background-color: #4b6584;
  color: aliceblue;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

.tree {
  position: fixed;
}
</style>
