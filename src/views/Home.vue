<template>
  <div class="home">
    <button @click="openWorkBench">workBench</button>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router';
const router = useRouter();
function openWorkBench(){
  const id = '1';
  const {href} = router.resolve({name:'workbench',query:{id}})
  window.open(href,'_blank')
}
</script>

<style scoped>
</style>
