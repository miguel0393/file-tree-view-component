<template>
  <div @contextmenu="(e) => e.preventDefault()">
    <div v-if="!treeIsEmpty">
      <div class="node" :style="{ 'margin-left': depth * 20 + 'px' }" @contextmenu="handleContextMenu($event)" @dblclick="nodeClicked" >
        <span unselectable="on" v-if="hasChildren" class="type" v-bind:class="{expanded: expanded, collapsed: !expanded}"></span>
        <span unselectable="on" v-else class="file-node"></span>
        <span unselectable="on" class="node-name" :style="getStyle(node)">{{ node.name }}</span>
      </div>

      <div class="node-children" v-if="expanded">
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
      <button v-on:click="addRootName">Create tree</button>
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
      this.$emit("setRootName");
    },
    handleContextMenu(e) {
      e.preventDefault();
      //Root Node
      if (this.depth === 0) {
        this.$emit("onRightClick",e, this, 'root');
      }
      //Folder
      if (this.depth > 0 && this.node.children) {
        this.$emit("onRightClick",e, this, 'folder');
      }
      //File
      if (this.depth > 0 && !this.node.children) {
        this.$emit("onRightClick",e, this, 'file');
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
#tree-viewer {
  /* width: 20%; */
  /* height: 100%; */
  /* background-color: #2c3e50; */
}

.node {
  text-align: left;
  font-size: 16px;
  /* width: 100%; */
  overflow-x: visible;
  -moz-user-select: none;
  -webkit-user-select: none;
  -ms-user-select: none;
  -o-user-select: none;
  user-select: none;
  padding: 5px 0px;
}

.container {
  margin: 5px;
  width: 100%;
}

.type {
  margin-right: 5px;
}

.collapsed, .expanded, .file-node, .node-name{
  height: 28px;
  width: 28px;
  display: inline-block;
  /* vertical-align: middle; */
}

.node-name{
  width: 50%;
}

.collapsed:before, .expanded:before, .file-node:before{
  content: '';
  display: inline-block;
  background-size: 28px 28px;
  height: 28px;
  width: 28px;
}

.collapsed:before{
  background-image: url('../assets/folder.svg');
}

.expanded:before{
  background-image: url('../assets/openfolder.svg');
}

.file-node:before{
  background-image: url('../assets/file.svg');
}
</style>
