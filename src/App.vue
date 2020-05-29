<template>
  <div id="app">
    <h1>Vue Tree Browser</h1>
    <TreeBrowser class="tree" :node="root" @onClick="nodeWasClicked"  @treeUpdated="treeWasUpdated" />
    <!-- <FileContent :content="content" /> -->
  </div>
</template>

<script>
import TreeBrowser from "./components/TreeBrowser.vue";
// import FileContent from "./components/FileContent.vue";

export default {
  name: "App",
  props: {
    content: {
      type: String,
      default: "CONTENIDO DEL ARCHIVO AQUÍ",
    },
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
    }
  },
  components: {
    TreeBrowser,
    // FileContent
  },
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
