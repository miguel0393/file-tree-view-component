<template>
  <div id="app" @contextmenu="(e) => e.preventDefault()">
    <div class="container" v-if="!treeIsEmpty">
      <div class="node" :style="{ 'margin-left': depth * 20 + 'px' }" @contextmenu="handleContextMenu($event)" @click="nodeClicked" >
        <span v-if="hasChildren" class="type">{{expanded ? '&#9660;' : '&#9658;'}}</span>
        <span v-else class="type">&#9671;</span>
        <span :style="getStyle(node)">{{ node.name }}</span>
      </div>

      <div v-if="expanded">
        <TreeBrowser
          v-for="child in node.children"
          :key="child.name"
          :node="child"
          :depth="depth + 1"
          @onClick="(node) => $emit('onClick', node)"
          @treeUpdated="() => $emit('treeUpdated', '')"
          @onRightClick="(e, target, type) => $emit('onRightClick',e, target, type)"
        />
      </div>
    </div>
    <div v-else>
      <p>Empty tree</p>
      <input v-model="rootName">
      <button v-on:click="addRootName">Add Element</button>
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
    }
  },
  data() {
    return {
      expanded: false,
      rootName: '',
    };
  },
  methods: {
    nodeClicked() {
      this.expanded = !this.expanded;
      if (!this.hasChildren) {
        // this.$set(this.node, "children", [
        //   {
        //     name: "newchildren.js",
        //     content: "New Added Children"
        //   }
        // ]);
        this.$emit("onClick", this.node);
      }
      this.$emit("treeUpdated", "");
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
        this.$emit("treeUpdated", "");
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
    treeIsEmpty(){
        return Object.keys(this.node).length === 0
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
