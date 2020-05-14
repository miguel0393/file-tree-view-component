<template>
  <div id="app">
    <div class="container">
      <div @click="nodeClicked" :style="{'margin-left': depth * 20 + 'px'}" class="node">
        <span v-if="hasChildren" class="type">{{expanded ? '&#9660;' : '&#9658;'}}</span>
        <span v-else class="type">&#9671;</span>
        <span :style="getStyle(node)">{{node.name}}</span>
      </div>

      <div v-if="expanded">
        <TreeBrowser
          v-for="child in node.children"
          :key="child.name"
          :node="child"
          :depth="depth + 1"
          @onClick="(node) => $emit('onClick', node)"
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
          this.$emit('onClick', this.node);
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

.container {
  margin: 5px;
  width: 100%;
}

.node {
  text-align: left;
  font-size: 16px;
  width: 100%;
  cursor: pointer;
}

.type {
  margin-right: 5px;
}
</style>