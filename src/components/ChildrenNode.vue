<template>
  <li>
    <!-- parent node -->
    <div class="tf-nc" @click="addNode(node.id)">
      <div>{{ node.title }}</div>
      <div v-for="(desc, index) in node.desc" :key="index">
        {{ desc }}
      </div>
    </div>
    <!-- children node -->
    <ul v-if="node.children.length > 0">
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
export default {
  name: 'ChildrenNode',
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
.tf-nc {
  border-radius: 4px;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
.tf-nc:hover {
  color: #fff;
  background: rgb(42, 116, 252);
}
</style>
