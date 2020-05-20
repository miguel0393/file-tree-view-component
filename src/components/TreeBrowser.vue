<template>
  <div id="app" @contextmenu="(e) => e.preventDefault()">
    <div class="container">
      <div
        class="node"
        :style="{'margin-left': depth * 20 + 'px'}"
        @contextmenu="handleContextMenu($event)"
        @click="nodeClicked"
      >
        <span class="type" v-if="hasChildren">{{expanded ? '&#9660;' : '&#9658;'}}</span>
        <span class="type" v-else>&#9671;</span>
        <span :style="getStyle(node)">{{node.name}}</span>
      </div>

      <div v-if="expanded">
        <TreeBrowser
          v-for="child in node.children"
          :key="child.name"
          :node="child"
          :depth="depth + 1"
          @onClick="(node) => $emit('onClick', node)"
          @onRightClick="(e) => $emit('onRightClick', e)"
        />
      </div>
    </div>
  </div>
</template>

<script>
// import * as ColorHash from "color-hash";
// const colorHash = new ColorHash();

export default {
  name: "TreeBrowser",
  props: {
    node: Object,
    depth: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      expanded: false
    };
  },
  methods: {
    nodeClicked() {
      this.expanded = !this.expanded;
      if (!this.hasChildren) {
        this.$emit("onClick", this.node);
      }
    },
    getStyle(node) {
      let color = "#e74c3c";
      if (!node.children) {
        // color = colorHash.hex(node.name.split(".")[1]);
        color = "#ecf0f1";
      }
      return {
        color
      };
    },
    handleContextMenu(e) {
      e.preventDefault();

      this.$emit("onRightClick", e);
    }
  },
  computed: {
    hasChildren() {
      return this.node.children;
    }
  }
};
</script>

<style scoped>
#app {
  width: 20%;
  height: 100%;
  background-color: #2c3e50;
}

.node {
  text-align: left;
  font-size: 16px;
  width: 100%;
  cursor: pointer;
}

.container {
  margin: 5px;
  width: 100%;
}

.type {
  margin-right: 5px;
}
</style>