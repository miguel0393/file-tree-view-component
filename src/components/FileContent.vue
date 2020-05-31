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
#file-content {
  background-color: #34495e;
  display: inline-block;
  width: 50%;
  display: inline-block;
}

.content {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 18px;
  text-align: left;
  margin: 20px;

}
</style>