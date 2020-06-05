<template>
  <div id="modal-window">
    <transition name="fade" appear>
      <div class="modal">
        <h1>{{title}}</h1>
        <!-- <p>{{description}}</p> -->

        <input v-focus type="text" placeholder="Name..." v-model="inputName"/>
        <textarea
          placeholder="File content..."
          resize="false"
          v-if="showTextArea"
          v-model="inputContent"
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
      inputName: this.elementName,
      inputContent: this.elementContent
    }
  },
  methods: {
    okButtonClicked() {
      this.$emit("onOkClick", this.inputName, this.inputContent);
    },
    cancelButtonClicked() {
      this.$emit("onCancelClick", this.newName);
    }
  },
  directives: {
  focus: {
    // directive definition
    inserted: function (el) {
      el.focus()
    }
  }
}
};
</script>

<style scoped>

@import '../assets/styles/modal.css';
</style>