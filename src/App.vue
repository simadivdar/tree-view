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
        label: "root",
        children: [],
      },
      count: 1,
    };
  },
  methods: {
    addFolder(node, label) {
      console.log("addFolder", node, label);
      this.count++;
      node.children.push({ id: this.count, label: label, children: [] });
    },
    addFile(node, label) {
      console.log("addFile", node, label);
      this.count++;
      node.children.push({ id: this.count, label: label });
    },
    deleteNode(node) {
      console.log("deleteNode", node);
      let child = this.node.children;
      this.DeletedNode(child,node);
    },
    DeletedNode(child,node){
      if(Array.prototype.includes.call(child,node)){
      const index = child.indexOf(node);
      child.splice(index,1);
      return;
      }
      else{
        for(let i=0;i<child.length;i++){
        if(child[i].children){
          this.DeletedNode(child[i].children,node);
        }
        else{
          continue;
        }
        }
      }
    }
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
