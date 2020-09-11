<template>
  <el-tooltip placement="top">
    <div slot="content">
      <div>{{ node.title }}</div>
      <div v-for="(desc, index) in node.desc" :key="index">
        {{ desc }}
      </div>
    </div>
    <div class="tf-nc" @click="addNode(node.id)">
      <div>{{ node.title }}</div>
    </div>
  </el-tooltip>
</template>

<script>
export default {
  name: 'ParentNode',
  props: {
    node: {
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
