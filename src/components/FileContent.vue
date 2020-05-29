<template>
  <div id="app">
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
#app {
  background-color: #34495e;
  display: inline-block;
  width: 74%;
  height: 100%;
  margin-left: 23%;
  margin-right: 3%;
}

.content {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 18px;
  text-align: left;
  margin: 20px;

}
</style>