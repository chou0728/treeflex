<template>
  <div class="tf-tree tf-custom tf-gap-lg" v-loading="loading">
    <ul>
      <li>
        <!-- parent node -->
        <ParentNode :node="treeData" @node-click="handleNodeClick" />
        <!-- children node -->
        <ul>
          <ChildrenNode
            v-for="key in treeData.children"
            :key="key"
            :childrenMap="treeData.childrenMap"
            :node="treeData.childrenMap[key]"
            @node-click="handleNodeClick"
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
      loading: false,
      treeData: {},
      cacheTreeDataMap: new Map()
    }
  },
  created() {
    this.loading = true
    this.fetchInitData()
      .then(data => {
        this.treeData = JSON.parse(JSON.stringify(data))
        this.cacheTreeDataMap.set(data.id, data)
      })
      .finally(() => {
        this.loading = false
      })
  },
  methods: {
    handleNodeClick(childKey) {
      // 點擊該節點 => 1.該節點沒抓過資料，則要去call api  2.該節點已經有抓過資料了，判斷是要打開還是收起來
      if (!this.cacheTreeDataMap.has(childKey)) {
        this.addNode(childKey)
        return
      }

      // 點擊的當下，查看一下該節點目前children裡面是否為空 => 1.不為空則代表要收起來 2.為空代表要準備去打開
      if (this.treeData.childrenMap[childKey].children.length > 0) {
        this.removeNode(childKey)
        return
      }

      this.addNodeFromCache(childKey)
    },
    addNodeFromCache(childKey) {
      console.log('addNodeFromCache')
      const currentNode = this.treeData.childrenMap[childKey]
      const cacheNode = this.cacheTreeDataMap.get(childKey)
      cacheNode.children.forEach(key => {
        currentNode.children.push(key)
      })
    },
    removeNode(childKey) {
      const currentNode = this.treeData.childrenMap[childKey]
      currentNode.children.splice(0, currentNode.children.length)
    },
    fetchInitData() {
      return new Promise(resolve => {
        const data = {
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
        setTimeout(() => resolve(data), 500)
      })
    },
    fetchNode() {
      return new Promise(resolve => {
        const data = {
          id: '1-2',
          title: 'test-1-2',
          desc: ['体育: 0.00%'],
          children: [
            '1-2-1',
            '1-2-2',
            '1-2-3',
            '1-2-4',
            '1-2-5',
            '1-2-6',
            '1-2-7',
            '1-2-8',
            '1-2-9',
            '1-2-10',
            '1-2-11',
            '1-2-12'
          ],
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
            },
            '1-2-3': {
              id: '1-2-3',
              title: 'test-1-2-3',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-4': {
              id: '1-2-4',
              title: 'test-1-2-4',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-5': {
              id: '1-2-5',
              title: 'test-1-2-5',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-6': {
              id: '1-2-6',
              title: 'test-1-2-6',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-7': {
              id: '1-2-7',
              title: 'test-1-2-7',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-8': {
              id: '1-2-8',
              title: 'test-1-2-8',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-9': {
              id: '1-2-9',
              title: 'test-1-2-9',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-10': {
              id: '1-2-10',
              title: 'test-1-2-10',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-11': {
              id: '1-2-11',
              title: 'test-1-2-11',
              desc: ['体育: 0.00%'],
              children: []
            },
            '1-2-12': {
              id: '1-2-12',
              title: 'test-1-2-12',
              desc: ['体育: 0.00%'],
              children: []
            }
          }
        }
        setTimeout(() => resolve(data), 500)
      })
    },
    addNode(childKey) {
      this.loading = true
      this.fetchNode()
        .then(data => {
          const { childrenMap } = data
          this.cacheTreeDataMap.set(data.id, data)
          Object.keys(childrenMap).forEach(key => {
            this.treeData.childrenMap[childKey].children.push(key)
            this.treeData.childrenMap[key] = childrenMap[key]
            this.cacheTreeDataMap.set(key, childrenMap[key])
          })
        })
        .finally(() => {
          this.loading = false
        })
    }
  }
}
</script>
<style>
.tf-custom {
  /* width: 500px; */
  font-size: 10px;
}
.tf-custom .tf-nc {
  height: 5em;
  line-height: 5em;
  /* width: 6em; */
  color: #fff;
  background-color: dodgerblue;
  border-color: dodgerblue;
  border-width: 2px;
  padding: 0;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
  text-align: center;
}

.tf-custom .tf-nc:hover {
  color: dodgerblue;
  background: #fff;
}

.tf-custom .tf-nc .title {
  width: 6em;
  padding: 0 4px;
  font-size: 12px;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

/* make the horizontal and vertical connectors thick and change their color */

.tf-custom .tf-nc:before,
.tf-custom .tf-nc:after {
  border-left-color: dodgerblue;
  border-left-width: 2px;
}

.tf-custom li li:before {
  border-top-color: dodgerblue;
  border-top-width: 2px;
}

/* fade */
.fade-leave-active,
.fade-enter-active {
  transition: all 0.3s;
}

.fade-enter {
  opacity: 0;
}

.fade-leave-to {
  opacity: 0;
}
</style>
