<template>
  <div class="tf-tree tf-gap-sm">
    <ul>
      <li>
        <!-- parent node -->
        <ParentNode :node="treeData" @node-click="addNode" />
        <!-- children node -->
        <ul>
          <ChildrenNode
            v-for="key in treeData.children"
            :key="key"
            :childrenMap="treeData.childrenMap"
            :node="treeData.childrenMap[key]"
            @node-click="addNode"
          />
        </ul>
      </li>
    </ul>
  </div>
</template>

<script>
import 'treeflex/dist/css/treeflex.css'
import ParentNode from './ParentNode'
import ChildrenNode from './ChildrenNode'

export default {
  name: 'TreeFlexMap',
  components: {
    ParentNode,
    ChildrenNode
  },
  data() {
    return {
      treeData: {
        id: '1',
        title: 'test-1',
        desc: ['体育: 0.00%'],
        children: ['1-1', '1-2'],
        childrenMap: {
          '1-1': {
            id: '1-1',
            title: 'test-1-1',
            desc: ['体育: 0.00%'],
            children: []
          },
          '1-2': {
            id: '1-2',
            title: 'test-1-2',
            desc: ['体育: 0.00%'],
            children: []
          }
        }
      }
    }
  },
  methods: {
    addNode(childKey) {
      const currentNode = this.treeData.childrenMap[childKey]
      // 抓取currentNode底下該有的Child資料
      const data = {
        id: '1-2',
        title: 'test-1-2',
        desc: ['体育: 0.00%'],
        children: ['1-2-1', '1-2-2'],
        childrenMap: {
          '1-2-1': {
            id: '1-2-1',
            title: 'test-1-2-1',
            desc: ['体育: 0.00%'],
            children: []
          },
          '1-2-2': {
            id: '1-2-2',
            title: 'test-1-2-2',
            desc: ['体育: 0.00%'],
            children: []
          }
        }
      }

      this.treeData.childrenMap = {
        ...this.treeData.childrenMap,
        ...data.childrenMap
      }

      Object.keys(data.childrenMap).forEach(key => {
        currentNode.children.push(key)
      })
    }
  }
}
</script>
