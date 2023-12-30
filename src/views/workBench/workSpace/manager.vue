<template>
    <div class="mi-manager__container">
      <sourceTree :tree-data="treeData" @node-click="nodeClick"></sourceTree>
    </div>
    
</template>

<script>
import sourceTree from '@/components/sourceTree.vue'
const treeData = [
  { id: 1, name: '一级1' },
  {
    id: 2,
    name: '一级2',
    children: [
      { id: 3, name: '二级2-1jjjjjjjjj' },
      { id: 4, name: '二级2-2' }
    ]
  },
  {
    id: 5,
    name: '一级3',
    children: [
      {
        id: 6,
        name: '二级3-1',
        children: [
          { id: 7, name: '三级3-1-1' },
          { id: 8, name: '三级3-1-2' }
        ]
      }
    ]
  }
]

export default {
  name:'manager',
  components:{
    sourceTree
  },
  data(){
    return {
      treeData:treeData
    }
  },
  methods:{
    nodeClick(val){
      console.log(val);
    }
  }
};
</script>


<style>
.mi-manager__container{
    height: 100%;
    width: 100%;
    margin: 0%;
    padding: 0%;
    background-color:#E3E3E3;
}
</style>

