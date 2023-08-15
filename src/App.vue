<script>
import { toRaw, toRefs } from "vue";
import TreeView from "./components/TreeView.vue";
export default {
  components: {
    TreeView,
  },
  data() {
    return {
      node: {
        id: 1,
        parentId: null,
        label: "root",
        children: [],
      },
      countId: 1,
      countParentId: 0,
    };
  },
  methods: {
    addFolder(node, label) {
      console.log("addFolder", node, label);
      this.countId++;
      this.countParentId = node.parentId;
      this.countParentId++;
      node.children.push({
        id: this.countId,
        parentId: this.countParentId,
        label: label,
        children: [],
      });
    },
    addFile(node, label) {
      console.log("addFile", node, label);
      this.countId++;
      this.countParentId = node.parentId;
      this.countParentId++;
      node.children.push({
        id: this.countId,
        parentId: this.countParentId,
        label: label,
      });
      console.log(this.node);
    },
    deleteNode(node) {
      console.log("deleteNode", node);
      let child = this.node.children;
      this.DeletedNode(child, node);
    },
    /* DeletedNode(child, node) {
      if (child.includes(node)) {
        const index = child.indexOf(node);
        child.splice(index, 1);
      } else {
        for (let i = 0; i < child.length; i++) {
          if (child[i].children) {
            this.DeletedNode(child[i].children, node);
          }
        }
      }
    },*/
    DeletedNode(child, node) {
      let parent = node.parentId;
      let id = node.id;
      for (let i = 0; i < child.length; i++) {
        if (child[i].parentId === parent && child[i].id === id) {
          const index = child.indexOf(child[i]);
          child.splice(index, 1);
          return;
        } else {
          if (child[i].children) {
            this.DeletedNode(child[i].children, node);
          }
        }
      }
    },
  },
};
</script>

<template>
  <main>
    <h2>Tree View</h2>
    <TreeView
      :node="node"
      @addFolder="addFolder"
      @addFile="addFile"
      @deleteNode="deleteNode"
    />
  </main>
</template>

<style>
main {
  max-width: 600px;
  margin: 0 auto;
}
</style>
