<template>
  <div class="tf-tree tf-gap-sm">
    <ul>
      <li>
        <!-- parent node -->
        <ParentNode :node="treeData" @node-click="addNode" />
        <!-- children node -->
        <ul>
          <ChildrenNode
            v-for="(children, index) in treeData.children"
            :key="index"
            :node="children"
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
  name: 'TreeFlex',
  components: {
    ParentNode,
    ChildrenNode
  },
  data() {
    return {
      treeData: {
        id: '1',
        title: 'test-1',
        desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
        children: [
          {
            id: '1-1',
            title: 'test-1-1',
            desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
            children: [
              {
                id: '1-1-1',
                title: 'test-1-1-1',
                desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
                children: []
              }
            ]
          },
          {
            id: '1-2',
            title: 'test-1-2',
            desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
            children: [
              {
                id: '1-2-1',
                title: 'test-1-2-1',
                desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
                children: [
                  {
                    id: '1-2-1-1',
                    title: 'test-1-2-1-1',
                    desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
                    children: [
                      {
                        id: '1-2-1-1-1',
                        title: 'test-1-2-1-1-1',
                        desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
                        children: []
                      }
                    ]
                  }
                ]
              }
            ]
          }
        ]
      }
    }
  },
  methods: {
    addNode(id) {
      const targetNode = this.findNode(this.treeData.children, id)
      targetNode.children.push({
        id: '1-2-1-1-1-1',
        title: 'test-1-2-1-1-1-1',
        desc: ['体育: 0.00%', '彩票: 0.00%', '真人: 0.00%', '棋牌: 0.00%', '小游戏: 0.00%'],
        children: []
      })
    },
    findNode(nodes, id) {
      let result = null
      result = nodes.find(node => node.id === id)
      if (!result) {
        nodes.forEach(childNode => {
          result = this.findNode(childNode.children, id)
        })
      }
      return result
    }
  }
}
</script>
