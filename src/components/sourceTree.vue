<template>
    <div class="mi-sourceTree-item">
      <div v-for="item in treeData" :key="item.id">
        <div class="item-title" @click="nodeClick(item)">
          <span>{{ item.name }}</span>
          <span v-if="item.children && item.children.length">
            [{{ isOpen(item.id) ? '-' : '+' }}]
          </span>
        </div>
        <div
          v-if="item.children && item.children.length"
          v-show="isOpen(item.id)"
          class="item-childen"
        >
          <sourceTree
            :treeData="item.children"
            @node-click="$emit('node-click', $event)"
          ></sourceTree>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { SheetInstance } from '@/adapter/sheetify';
  export default {
    name: 'sourceTree',
    props: {
      treeData: {
        type: Array,
        default: () => []
      }
    },
    data() {
      return {
        expandedKeys: [] // 当前展开的节点id组成的数组
      }
    },
    methods: {
      nodeClick(item) {
        this.$emit('node-click', item)
        if (item.children && item.children.length) {
          let index = this.expandedKeys.indexOf(item.id)
          if (index > -1) {
            // 如果当前节点id存在数组中，则删除
            this.expandedKeys.splice(index, 1)
          } else {
            // 如果当前节点id不存在数组中，则添加
            this.expandedKeys.push(item.id)
          }
        }
        SheetInstance.spreadsheet.addSheet(item.name,true);
      },
      isOpen(id) {
        // 判断节点id在不在数组中，在则显示，不在则隐藏
        return this.expandedKeys.includes(id)
      }
    }
  }
  </script>
  
  <style  scoped>
  .mi-sourceTree-item {
    cursor: pointer;
    .item-title {
      padding: 4px 8px;
      &:hover {
        background-color: #1A7B42;
      }
    }
    .item-childen {
      padding-left: 20px;
    }
  }
  </style>
  
