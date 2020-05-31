<template>
  <div id="app" @click="onClick">
    <h1>Files Tree-View Component</h1>
    <div id="tree-container">
      <TreeBrowser
      id="tree"
      :node="root"
      :treeIsEmpty="Object.keys(this.root).length === 0"
      :expanded="expandedTree"
      @onClick="nodeWasClicked"
      @onRightClick="showContextMenu"
      @treeUpdated="treeWasUpdated"
      @setRootName="setRootName"
    />

    <FileContent :content="content" />

    <ContextMenu
      :xPosition="contextMenuXPosition"
      :yPosition="contextMenuYPosition"
      :visible="contextMenuIsVisible"
      @onClick="handleMenuOperation"
      :menuType="contextMenuType"
    />

    <ModalDialog v-if="modalDialogIsVisible"
      :visible="modalDialogIsVisible"
      :title="modalTitle"
      :showTextArea="modalShowTextArea"
      :elementName="modalCurrentName"
      :elementContent="modalCurrentContent"
      @onOkClick="hideModalDialog"
      @onCancelClick="() => this.modalDialogIsVisible = false"
    />
  </div>
    </div>
    
</template>

<script>
import TreeBrowser from "./TreeBrowser.vue";
import FileContent from "./FileContent.vue";
import ContextMenu from "./ContextMenu.vue";
import ModalDialog from "./ModalDialog.vue";

export default {
  name: "TreeController",
  props: { },
  data() {
    return {
      root: {},
      content: '',
      contextMenuType: "",
      contextMenuXPosition: 0,
      contextMenuYPosition: 0,
      contextMenuIsVisible: false,
      currentOperation: null,
      currentNode: null,
      modalDialogIsVisible: false,
      modalTitle: "Cambiar Nombre",
      modalShowTextArea: false,
      modalCurrentName: null,
      modalCurrentContent: null,
      expandedTree: false
    };
  },
  created() {
    if (localStorage.treeStructure) {
      this.root = JSON.parse(localStorage.treeStructure);
    }
  },
  methods: {
    nodeWasClicked(node) {
      this.expandedTree = true;
      this.content = node.content;
    },
    treeWasUpdated() {
      this.expandedTree = true;
      localStorage.treeStructure = JSON.stringify(this.root);
    },
    setRootName(){
      this.expandedTree = true;
      this.currentOperation = 'set-root-name';
      this.showModalDialog('Set tree name', false)
    },
    showContextMenu(e, target, type) {
      this.expandedTree = true;
      this.currentNode = target;
      this.contextMenuType = type;
      this.contextMenuXPosition = e.x;
      this.contextMenuYPosition = e.y;
      this.contextMenuIsVisible = true;
    },
    showModalDialog(title, showTextArea, currentName, currentContent) {
      this.modalDialogIsVisible = true;
      this.modalTitle = title;
      this.modalShowTextArea = showTextArea;
      
      this.modalCurrentName = currentName;
      this.modalCurrentContent = currentContent;
    },
    hideModalDialog(newName, newContent) {
      this.modalDialogIsVisible = false;

      switch (this.currentOperation) {
        case "add-subfolder":
            this.currentNode.node.children.push({
              name: newName,
              children: []
            });
          break;

          case "add-file":
            this.currentNode.node.children.push({
              name: newName,
              content: ""
            });
          break;

          case "modify-file":
            this.$set(this.currentNode.node, "name", newName);
            this.$set(this.currentNode.node, "content", newContent);
            this.content = this.currentNode.node.content;
          break;

          case "set-root-name":
            this.$set(this.root, 'name', newName)
            this.$set(this.root, 'children', [])
          break;
      }

      this.treeWasUpdated();
    },
    onClick() {
      this.contextMenuIsVisible = false;
    },
    deleteTree() {
      localStorage.treeStructure = JSON.stringify({});
      this.root = JSON.parse(localStorage.treeStructure);
    },
    deleteNode(parent, child) {
      //Find index for child we want to delete
      var index;
      for (let i = 0, len = parent.$children.length; i < len; i++) {
        if (parent.$children[i]._uid === child._uid) {
          index = i;
          break;
        }
      }
      parent.$children.splice(index,1);
      this.$set(parent.node, 'children', parent.$children.map(child => child.node));
      this.treeWasUpdated();
    },
    handleMenuOperation(operation) {
      this.contextMenuIsVisible = false;
      this.modalCurrentName = "",
      this.modalCurrentContent = ""
      this.currentOperation = operation;

      switch (operation) {
        case "delete-tree":
          this.deleteTree();
          break;

        case "add-subfolder":
          this.showModalDialog("Add Subfolder", false);
          break;

        case "delete-subfolder":
          this.deleteNode(this.currentNode.$parent, this.currentNode);
          break;

        case "add-file":
          this.showModalDialog("Add File", false);
          break;

        case "delete-file":
          this.deleteNode(this.currentNode.$parent, this.currentNode);
          break;

        case "modify-file":
           this.showModalDialog("Modify File", true, this.currentNode.node.name, this.currentNode.node.content);
          break;

        default:
          break;
      }
    }
  },
  computed:{
    treeIsEmpty(){
     return Object.keys(this.root).length === 0
    }
  },
  components: {
    TreeBrowser,
    FileContent,
    ContextMenu,
    ModalDialog
  }
};
</script>

<style>

@import '../assets/styles/tree-controller.css';

</style>
