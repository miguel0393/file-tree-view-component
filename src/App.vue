<template>
  <div id="app">
    <h1>File Tree-View Component</h1>
    <FileTreeVisualizer :showFolderOpt="false"/>
  </div>
    
</template>

<script>
import FileTreeVisualizer from "./components/FileTreeVisualizer.vue";

export default {
  name: "App",
  props: { },
  components: {
    FileTreeVisualizer
  }
};
</script>

<style></style>
