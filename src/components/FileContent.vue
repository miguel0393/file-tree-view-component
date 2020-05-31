<template>
  <div id="file-content">
    <div class="content">
      <section>
          {{content}}
      </section>
    </div>
  </div>
</template>

<script>
export default {
    name: "FileContent",
    props: {
        content: String
    },
};
</script>

<style scoped>

@import '../assets/styles/file-content.css';
</style>