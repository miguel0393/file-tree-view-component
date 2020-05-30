<template>
  <div id="app" @click="onClick">
    <h1>Files Tree-View Component</h1>

    <TreeBrowser
      class="tree"
      :node="root"
      @onClick="nodeWasClicked"
      @onRightClick="showContextMenu"
      @treeUpdated="treeWasUpdated"
    />

    <FileContent :content="content" />

    <ContextMenu
      :xPosition="contextMenuXPosition"
      :yPosition="contextMenuYPosition"
      :visible="contextMenuIsVisible"
      @onClick="handleMenuOperation"
      :menuType="contextMenuType"
    />
    <ModalDialog
      :visible="modalDialogIsVisible"
      :title="modalTitle"
      :description="modalDescription"
      @onClick="hideModalDialog"
    />
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
    modalDialogIsVisible: {
      type: Boolean,
      default: false
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
      contextMenuType: "",
      contextMenuXPosition: 0,
      contextMenuYPosition: 0,
      contextMenuIsVisible: false,
      currentOperation: null,
      currentNode: null
    };
  },
  created() {
    if (localStorage.treeStructure) {
      this.root = JSON.parse(localStorage.treeStructure);
    }
  },
  methods: {
    nodeWasClicked(node) {
      this.content = node.content;
    },
    treeWasUpdated() {
      localStorage.treeStructure = JSON.stringify(this.root);
    },
    showContextMenu(e, target, type) {
      this.currentNode = target;
      this.contextMenuType = type;
      this.contextMenuIsVisible = true;
      this.contextMenuXPosition = e.x;
      this.contextMenuYPosition = e.y;
    },
    showModalDialog(title, description) {
      this.modalDialogIsVisible = true;
      this.modalTitle = title;
      this.modalDescription = description;
    },
    hideModalDialog() {
      this.modalDialogIsVisible = false;
    },
    onClick() {
      this.contextMenuIsVisible = false;
    },
    deleteTree(){
      localStorage.treeStructure = JSON.stringify({});
      this.root = JSON.parse(localStorage.treeStructure);
    },
    handleMenuOperation(operation){
      this.contextMenuIsVisible = false;
      this.currentOperation = operation;
      switch (operation) {
        case 'delete-tree':
          this.deleteTree()
          break;
        case 'add-subfolder':
          break;
        case 'toggle-expand-tree':
          
          break;
        case 'delete-subfolder':
          
          break;
        case 'add-file':
          
          break;
        case 'toggle-expand-node':
          
          break;
        case 'delete-file':
             
          break;
        case 'modify-file':
          
          break;
        case 'show-file':
          
          break;
      
        default:

          break;
      }
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
