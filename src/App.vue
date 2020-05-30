<template>
  <div id="app" @click="onClick">
    <h1>Files Tree-View Component</h1>

    <TreeBrowser
      class="tree"
      :node="root"
      :treeIsEmpty="Object.keys(this.root).length === 0"
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
      :showTextArea="modalShowTextArea"
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
    modalShowTextArea: {
      type: Boolean,
      default: false
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
    showModalDialog(title, showTextArea) {
      this.modalDialogIsVisible = true;
      this.modalTitle = title;
      this.modalShowTextArea = showTextArea;
    },
    hideModalDialog(newName) {
      this.modalDialogIsVisible = false;
      console.log(this.currentNode.children);

      switch (this.currentOperation) {
        case "add-subfolder":
            this.currentNode.children.push({
              name: newName,
              children: []
            });
          break;

          case "add-file":
            this.currentNode.children.push({
              name: newName,
              children: [],
              content: ""
            });
          // }
          break;
      }

      this.treeWasUpdated();
    },
    onClick() {
      this.contextMenuIsVisible = false;
    },
    deleteTree() {
      localStorage.treeStructure = JSON.stringify({});
      this.root = JSON.parse(localStorage.treeStructure);
    },
    handleMenuOperation(operation) {
      this.contextMenuIsVisible = false;
      this.currentOperation = operation;

      switch (operation) {
        case "delete-tree":
          this.deleteTree();
          break;

        case "add-subfolder":
          this.showModalDialog("Add Subfolder", false);
          break;

        case "delete-subfolder":
          break;

        case "add-file":
          this.showModalDialog("Add File", true);
          break;

        case "delete-file":
          break;

        case "modify-file":
          this.showModalDialog("Add Subfolder", true);
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
