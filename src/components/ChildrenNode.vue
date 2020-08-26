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
