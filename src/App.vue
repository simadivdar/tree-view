<script>
import TreeView from './components/TreeView.vue';
export default {
    components: {
        TreeView,
    },
    data() {
        return {
            node: {
                id: 1,
                label: 'root',
                children: [
                    {
                        id: 2,
                        label: 'child 1',
                        children: [
                            {
                                id: 3,
                                label: 'child 1.1',
                            },
                            {
                                id: 4,
                                label: 'child 1.2',
                                children: [],
                            },
                        ],
                    },
                    {
                        id: 5,
                        label: 'child 2',
                        children: [],
                    }],
            },
            count:5,
        };
    },
    methods: {
        addFolder(node, label) {
            console.log('addFolder', node, label);
            this.count++;
            node.children.push({id:this.count,label: label, children:[]});
        },
        addFile(node, label) {
            console.log('addFile', node, label);
            // put your code here
        },
        deleteNode(node) {
            console.log('deleteNode', node);
            // put your code here
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

