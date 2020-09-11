<template>
  <li>
    <!-- parent node -->
    <ParentNode :node="node" @node-click="addNode" />
    <!-- children node -->
    <ul v-if="node.children.length > 0" class="child-wrap">
      <ChildrenNode
        v-for="key in node.children"
        :key="key"
        :childrenMap="childrenMap"
        :node="childrenMap[key]"
        @node-click="addNode"
      />
    </ul>
  </li>
</template>

<script>
import ParentNode from './ParentNode'

export default {
  name: 'ChildrenNode',
  components: {
    ParentNode
  },
  props: {
    node: {
      type: Object
    },
    childrenMap: {
      type: Object
    }
  },
  methods: {
    addNode(id) {
      this.$emit('node-click', id)
    }
  }
}
</script>
<style scoped>
/* .tf-nc {
  border-radius: 4px;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
.tf-nc:hover {
  color: #fff;
  background: dodgerblue;
} */

/* .child-wrap {
  border: 1px solid #f0f;
  position: relative;
}
.child-wrap::after {
  content: '';
  display: block;
  width: 1em;
  height: 1em;
  background: #f00;
  position: absolute;
  top: -1.2em;
  left: calc(50% - 0.5em);
  border-radius: 50%;
} */
</style>
