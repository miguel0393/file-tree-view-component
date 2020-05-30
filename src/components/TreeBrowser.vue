<template>
  <div id="app" @contextmenu="(e) => e.preventDefault()">
    <div class="container" v-if="!treeIsEmpty">
      <div class="node" :style="{ 'margin-left': depth * 20 + 'px' }" @contextmenu="handleContextMenu($event)" @dblclick="nodeClicked" >
        <span unselectable="on" v-if="hasChildren" class="type">{{expanded ? '&#9660;' : '&#9658;'}}</span>
        <span unselectable="on" v-else class="type">&#9671;</span>
        <span unselectable="on" :style="getStyle(node)">{{ node.name }}</span>
      </div>

      <div v-if="expanded">
        <TreeBrowser
          v-for="child in node.children"
          :key="child.name"
          :node="child"
          :depth="depth + 1"
          :treeIsEmpty="treeIsEmpty"
          :expanded="expandedChild"
          @onClick="(node) => $emit('onClick', node)"
          @treeUpdated="() => $emit('treeUpdated', '')"
          @onRightClick="(e, target, type) => $emit('onRightClick',e, target, type)"
        />
      </div>
    </div>
    <div v-else>
      <p>Empty tree</p>
      <input v-model="rootName">
      <button v-on:click="addRootName">Element</button>
    </div>
  </div>
</template>

<script>

export default {
  name: "TreeBrowser",
  props: {
    node: Object,
    depth: {
      type: Number,
      default: 0
    },
    treeIsEmpty: Boolean,
    expanded: Boolean,
  },
  data() {
    return {
      rootName:'',
      expandedChild: true,
    };
  },
  methods: {
    nodeClicked() {
      this.expanded = !this.expanded;
      if (this.depth != 0) {
        this.expandedChild = false;
        if (!this.hasChildren) {
          this.$emit("onClick", this.node);
        }
      }
      // this.$emit("treeUpdated", "");
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
    addRootName() {
      if (this.rootName !== '') {
        this.$set(this.node, 'name', this.rootName);
        this.$set(this.node, 'children', []);
        this.$emit("treeUpdated", "");
        this.treeIsEmpty = false;
      }
    },
    handleContextMenu(e) {
      e.preventDefault();
      //Root Node
      if (this.depth === 0) {
        this.$emit("onRightClick",e, this.node, 'root');
      }
      //Folder
      if (this.depth > 0 && this.node.children) {
        this.$emit("onRightClick",e, this.node, 'folder');
      }
      //File
      if (this.depth > 0 && !this.node.children) {
        this.$emit("onRightClick",e, this.node, 'file');
      }
    }
  },
  computed: {
    hasChildren() {
      if (this.node) {
        return this.node.children;
      } else {
        return false;
      }
    },
    // expandNodes() {
    //   if (this.depth > 0) {
    //     alert("raiz");
    //     return !this.expanded;
    //   } else {
    //     alert("hijo")
    //     return true;
    //   }
    // }
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

  overflow-x: visible;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
}

.container {
  margin: 5px;
  width: 100%;
}

.type {
  margin-right: 5px;
}
</style>
