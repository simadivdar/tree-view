<script>
export default {
    name: 'TreeView',
    props: {
        node: {
            type: Object,
            required: true,
        },
    },
    methods: {
        addFolder() {
            const label = prompt('Enter folder name');
            if (!label) return;
            this.$emit('addFolder', this.node, label);
        },
        addFile() {
            const label = prompt('Enter file name');
            if (!label) return;
            this.$emit('addFile', this.node, label);
        },
        deleteNode() {
            this.$emit('deleteNode', this.node);
        },
    },
};
</script>

<template>
  <div class="node">
      <div class="node__details">
          <div class="node__label">
              {{ node.label }}
              <small v-if="!node.children">(file)</small>
          </div>
          <div class="node__actions">
              <button v-if="node.children"  @click="addFolder">Add Folder</button>
              <button v-if="node.children"  @click="addFile">Add File</button>
              <button v-if="node.id !== 1"  @click="deleteNode">Delete</button>
          </div>
      </div>
      <div class="node__children">
          <TreeView
              v-bind="$attrs"
              v-for="subnode in node.children"
              :key="subnode.id"
              :node="subnode"
          />
      </div>
    </div>
</template>

<style lang="scss">
.node {
  padding: 8px 0 8px 8px;
  border-left: 2px solid #ddd;

  &:hover {
    border-color: #0ea4ea;
  }

  &__details {
    display: flex;
    align-items: center;
    margin-bottom: 10px;

    &:hover {
      background-color: #eee;
    }
  }

  &__label {
    flex: 1;
  }

  &__actions {
    button {
      cursor: pointer;
      margin-left: 8px;
    }
  }

  &__children {
    margin-left: 16px;
  }
}
</style>
