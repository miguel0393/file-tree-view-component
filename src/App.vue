<template>
  <div id="app" @click="onClick">
    <TreeController/>
  </div>
    
</template>

<script>
import TreeController from "./components/TreeController.vue";

export default {
  name: "App",
  props: { },
  components: {
    TreeController
  }
};
</script>

<style>

</style>
