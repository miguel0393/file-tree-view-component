<template>
  <div id="app">
    <transition name="fade" appear>
      <div class="modal" v-if="visible">
        <h1>{{title}}</h1>
        <!-- <p>{{description}}</p> -->

        <input type="text" autofocus placeholder="Name..." v-model="newName" />
        <textarea
          placeholder="File content..."
          resize="false"
          v-if="showTextArea"
          v-model="content"
        />
        <button @click="okButtonClicked">Ok</button>
        <button @click="cancelButtonClicked">Cancel</button>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  name: "ModalDialog",
  props: {
    title: String,
    showTextArea: {
      type: Boolean,
      default: false
    },
    newName: String,
    content: String,
    visible: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    okButtonClicked() {
      this.$emit("onClick", this.newName);
    },
    cancelButtonClicked() {
      this.visible = false;
    }
  }
};
</script>

<style scoped>
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 99;

  width: 100%;
  max-width: 400px;
  background-color: #fff;
  color: black;
  border-radius: 16px;
  padding: 25px;
}

.modal h1 {
  color: #222;
  font-size: 23px;
  font-weight: 900;
  margin-bottom: 15px;
}

.modal p {
  color: #666;
  font-size: 18px;
  font-weight: 400;
  margin-bottom: 15px;
}

.modal input[type="text"] {
  width: 100%;
  padding: 0.5rem;
}

.modal textarea {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  width: 100%;
  height: 200px;
  padding: 0.5rem;
  margin-top: 10px;
  resize: none;
}

.modal button {
  width: 30%;
  margin: 15px;
  padding: 0.5rem;
}
</style>