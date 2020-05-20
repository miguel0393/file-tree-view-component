<template>
  <div id="app" @click="onClick">
    <h1>Files Tree-View Component</h1>
    <TreeBrowser class="tree" :node="root" @onClick="nodeWasClicked" @onRightClick="showContextMenu" />
    <FileContent :content="content" />
    <ContextMenu :xPosition="xPosition" :yPosition="yPosition" :show="showCM"/>
    <ModalDialog />
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
    xPosition: Number,
    yPosition: Number,
    showCM: {
      type: Boolean,
      default: false
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
      this.showCM = true;
      this.xPosition = e.x;
      this.yPosition = e.y;
    },
    onClick() {
      this.showCM = false;
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
