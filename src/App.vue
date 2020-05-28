<template>
  <div id="app" @click="onClick">
    <h1>Files Tree-View Component</h1>
    
    <TreeBrowser class="tree" :node="root" @onClick="nodeWasClicked" @onRightClick="showContextMenu" />

    <FileContent :content="content" />

    <ContextMenu :xPosition="contextMenuXPosition" :yPosition="contextMenuYPosition" :visible="contextMenuIsVisible"
      @onClick="showModalDialog"
    />
    <ModalDialog :visible="modalDialogIsVisible" @onClick="hideModalDialog"/>
  </div>
</template>

<script>
import root from "./root.json";
import TreeBrowser from "./components/TreeBrowser.vue";
import FileContent from "./components/FileContent.vue";
import ContextMenu from "./components/ContextMenu.vue";
import ModalDialog from "./components/ModalDialog.vue";

export default {
  name: "App",
  props:{
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
    }
  },
  data() {
    return {
      root
    };
  },
  methods: {
    nodeWasClicked(node) {
      this.content = node.content;
    },
    showContextMenu(e) {
      this.contextMenuIsVisible = true;
      this.contextMenuXPosition = e.x;
      this.contextMenuYPosition = e.y;
    },
    showModalDialog() {
      this.contextMenuIsVisible = false;
      this.modalDialogIsVisible = true;
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
