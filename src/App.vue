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
      :elementName="modalCurrentName"
      :elementContent="modalCurrentContent"
      @onOkClick="hideModalDialog"
      @onCancelClick="() => this.modalDialogIsVisible = false"
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
      default: "Empty file..."
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
      currentNode: null,
      modalCurrentName: null,
      modalCurrentContent: null
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
    showModalDialog(title, showTextArea, currentName, currentContent) {
      this.modalDialogIsVisible = true;

      this.modalTitle = title;
      this.modalShowTextArea = showTextArea;
      this.modalCurrentName = currentName;
      this.modalCurrentContent = currentContent;
    },
    hideModalDialog(newName, newContent) {
      this.modalDialogIsVisible = false;

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
              content: ""
            });
          break;

          case "modify-file":
            this.$set(this.currentNode, "name", newName);
            this.$set(this.currentNode, "content", newContent);
            this.content = this.currentNode.content;
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
      this.modalCurrentName = "",
      this.modalCurrentContent = ""
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
          this.showModalDialog("Add File", false);
          break;

        case "delete-file":
          
          break;

        case "modify-file":
           this.showModalDialog("Modify File", true, this.currentNode.name, this.currentNode.content);
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
