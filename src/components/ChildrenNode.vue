<template>
  <li>
    <!-- parent node -->
    <ParentNode :node="node" @node-click="handleNodeClick" />

    <!-- children node -->
    <transition name="fade" mode="out-in">
      <ul v-if="node.children.length > 0" class="child-wrap">
        <ChildrenNode
          v-for="key in node.children"
          :key="key"
          :childrenMap="childrenMap"
          :node="childrenMap[key]"
          @node-click="handleNodeClick"
        />
      </ul>
    </transition>
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
    handleNodeClick(id) {
      this.$emit('node-click', id)
    }
  }
}
</script>
