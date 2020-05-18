<template>
  <div id="app">
    <h1>Vue Tree Browser</h1>
    <TreeBrowser class="tree" :node="root" @onClick="nodeWasClicked" @onRightClick="showContextMenu" />
    <FileContent :content="content" />
    <ContextMenu :xPosition="xPosition" :yPosition="yPosition" :show="show"/>
  </div>
</template>

<script>
import root from "./root.json";
import TreeBrowser from "./components/TreeBrowser.vue";
import FileContent from "./components/FileContent.vue";
import ContextMenu from "./components/ContextMenu.vue";

export default {
  name: "App",
  props:{
    content: {
      type: String,
      default: "CONTENIDO DEL ARCHIVO AQUÍ"
    },
    xPosition: Number,
    yPosition: Number,
    show: {
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
      this.show = !this.show;
      this.xPosition = e.x;
      this.yPosition = e.y;
    }
  },
  components: {
    TreeBrowser,
    FileContent,
    ContextMenu
  }
};
</script>

<style>

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
