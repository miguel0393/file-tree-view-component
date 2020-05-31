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
.custom-cm {
  text-align: left;
  color: black;
  background-color: aliceblue;
  border: 1px solid #cccccc;
  box-shadow: 1px 1px 10px rgb(0, 0, 0, 0.1);
  padding: 10px 0px;
  position: absolute;
  width: 200px;
}

.custom-cm__item {
  cursor: pointer;
  padding: 8px 15px;
}

.custom-cm__item:hover {
  background-color: antiquewhite;
}
</style>