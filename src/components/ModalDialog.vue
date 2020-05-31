<template>
  <div id="modal-window">
    <transition name="fade" appear>
      <div class="modal">
        <h1>{{title}}</h1>
        <!-- <p>{{description}}</p> -->

        <input type="text" autofocus placeholder="Name..." v-model="inputName" />
        <textarea
          placeholder="File content..."
          resize="false"
          v-if="showTextArea"
          v-model="elementContent"
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
    elementName: {
      type: String,
      default: ""
    },
    elementContent: {
      type: String,
      default: ""
    }
  },
  data(){
    return{
      inputName: this.elementName
    }
  },
  methods: {
    okButtonClicked() {
      this.$emit("onOkClick", this.inputName, this.elementContent);
    },
    cancelButtonClicked() {
      this.$emit("onCancelClick", this.newName);
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