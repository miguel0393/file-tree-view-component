<template>
  <div
    id="context-menu"
    class="custom-cm"
    v-if="visible"
    :style="{ 'top': yPosition + 'px', 'left': xPosition + 'px'}"
    @contextmenu="(e) => e.preventDefault()"
  >
    <div
      v-for="(option, index) in currentOptions"
      class="custom-cm__item"
      :key="index"
      @click="handleMenuClick(option.function)"
    >{{ option.name }}</div>

  </div>
</template>

<script>
export default {
  name: "ContextMenu",
  props: {
    visible: {
      type: Boolean,
      default: false
    },
    xPosition: {
      type: Number,
      default: 0
    },
    yPosition: {
      type: Number,
      default: 0
    },
    menuType: {
      type: String,
      default: ""
    }
  },
  data() {
    return {
      menuOptions: {
        root: [
          { name: "Add Subfolder", function: "add-subfolder" },
          { name: "Add file", function: "add-file" },
          { name: "Delete tree", function: "delete-tree" }          
        ],
        folder: [
          { name: "Add Subfolder", function: "add-subfolder" },
          { name: "Add file", function: "add-file" },
          { name: "Delete subfolder", function: "delete-subfolder" }
        ],
        file: [
          { name: "Modify file", function: "modify-file" },
          { name: "Delete file", function: "delete-file" }
        ]
      },
      currentOptions: [],
    };
  },
  methods: {
    handleMenuClick(option) {
        this.$emit('onClick', option);
    },
  },
  beforeUpdate() {
    if (this.menuType !== "") {
      this.currentOptions = this.menuOptions[this.menuType];
    }
  }
};
</script>

<style scoped>

@import '../assets/styles/context-menu.css';
</style>