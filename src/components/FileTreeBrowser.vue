<template>
  <div @contextmenu="(e) => e.preventDefault()">
    <div v-if="!treeIsEmpty">
      <div class="node" :style="{ 'margin-left': depth * 20 + 'px' }" @dblclick="nodeClicked" >
        <div class="elements"  @contextmenu="handleContextMenu($event)">
          <span unselectable="on" v-if="hasChildren" class="type" v-bind:class="{expanded: expandedRoot, collapsed: !expandedRoot}"></span>
          <span unselectable="on" v-else class="file-node"></span>
          <span unselectable="on" class="node-name" v-bind:class="{folder: hasChildren, file: !hasChildren}">{{ node.name }}</span>
        </div>
      </div>

      <div class="node-children" v-if="expandedRoot">
        <FileTreeBrowser
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
      <button id="create-tree-btn" v-on:click="addRootName">Create tree</button>
    </div>
  </div>
</template>

<script>

export default {
  name: "FileTreeBrowser",
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
      expandedRoot: this.expanded,
      expandedChild: true,
    };
  },
  methods: {
    nodeClicked() {
      this.expandedRoot = !this.expandedRoot;
      if (this.depth != 0) {
        this.expandedChild = false;
        if (!this.hasChildren) {
          this.$emit("onClick", this.node);
        }
      }
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
    }
  }
};
</script>

<style scoped>
  @import '../assets/styles/file-tree-browser.css';
</style>
