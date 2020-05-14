<template>
  <div id="app">
    <h1>Vue Tree Browser</h1>
    <TreeBrowser class="tree" :node="root" @onClick="nodeWasClicked" />
    <FileContent :content="content" />
  </div>
</template>

<script>
import root from "./root.json";
import TreeBrowser from "./components/TreeBrowser.vue";
import FileContent from "./components/FileContent.vue";

export default {
  name: "App",
  props:{
    content: {
      type: String,
      default: "CONTENIDO DEL ARCHIVO AQUÍ"
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
    }
  },
  components: {
    TreeBrowser,
    FileContent
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
