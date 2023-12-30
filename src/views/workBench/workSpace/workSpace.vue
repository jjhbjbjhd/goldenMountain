<template>
    <div class="mi-workSpace__main">
      <div class="mi-sideBar__main">
        <div
          :class="[active === index ? 'active' : '']"
          @click="switchTool(item, index)"
          class="sideTools"
          v-for="(item, index) in data"
          :key="index"
        >
          <div>{{ item.name }}</div>
        </div>
      </div>
      <component :is="currentComponent"></component>
    </div>
  </template>
  
  <script setup>
  import { ref, reactive, shallowRef,markRaw } from 'vue';
  import manager  from './manager.vue';
  import search from './search.vue'
  
  const data = reactive([
    {
        name:'资源',
        comId: markRaw(manager),
    },
    {
        name:'搜索',
        comId: markRaw(search)
    },
    {
        name:'版本'
    },
    {
        name:'评论'
    },
    {
        name:'批注'
    },
    {
        name:'数据库'
    },
    {
        name:'数据验证'
    }

  ]);
  
  const currentComponent = shallowRef(manager);
  const active = ref(0);
  
  const switchTool = (item, index) => {
    currentComponent.value = item.comId;
    active.value = index;
  };
  </script>
  
  <style scoped>

    .active {
      background-color: #F5F5F5;
      color: #1A7B42;
    }
  
    .mi-workSpace__main {
      height: 100%;
      background-color: white;
      display: flex;

      &:hover{
        cursor: pointer;
      }
  
      .mi-sideBar__main {
        background-color: #ebebeb;
        width: 50px;
        height: 100%;
      }
    }
  
    .sideTools {
      width: 40px;
      height: 60px;
      border-radius: 2%;
      margin-top: 40px;
      margin-bottom: 40px;
      font-size: 15px;
      font-weight: 500;
      text-align: center;
      line-height: 50px;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
  </style>
  