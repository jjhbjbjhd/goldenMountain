<template>
  <div class="box">
    <workSpace :style="{width: leftWidth}" :id="{ 'workSpaceTransition': isResizing }"></workSpace>    
    <div class="resize" title="收缩侧边栏"></div>
    <sheetContext :style="{width: `calc(100% - ${leftWidth})`}"></sheetContext>
  </div>
  <footerBar></footerBar>
</template>

<script setup>
import workSpace from "./workSpace/workSpace"
import sheetContext from "./sheetContext/sheetContext"
import footerBar from "./footerBar/footerBar"
import { ref, onMounted, watch } from 'vue';
import { SheetInstance } from '@/adapter/sheetify';

let leftWidth = ref('calc(100px + 10%)'); // 初始左侧宽度
let isResizing = ref(false);

function dragControllerDiv() {
  let resize = document.getElementsByClassName('resize');
  let workSpace = document.getElementsByClassName('mi-workSpace__main');
  let sheet = document.getElementsByClassName('mi-sheet');
  let box = document.getElementsByClassName('box');
  
  resize[0].onmousedown = function(e){
    isResizing.value = true;
    resize[0].style.background = '#1A7B42';
    let startX = e.clientX;
    resize[0].left = resize[0].offsetLeft;
    document.onmousemove = function(e){
      let endX = e.clientX;

      let moveLen = resize[0].left + (endX - startX);
      let maxT = box[0].clientWidth - resize[0].offsetWidth; // 容器宽度 - 左边区域的宽度 = 右边区域的宽度

      if (moveLen < 120) moveLen =  40; 
      if (moveLen > maxT - 150) moveLen = maxT - 150; 

      resize[0].style.left = moveLen
      workSpace[0].style.width = moveLen + 'px';
      sheet[0].style.width = (box[0].clientWidth - moveLen - 10) + 'px';
      leftWidth.value = moveLen + 'px';
    }

    document.onmouseup = function (e){
      //颜色恢复
      resize[0].style.background = '#E3E3E3';
      document.onmousemove = null;
      document.onmouseup = null;
      resize[0].releaseCapture && resize[0].releaseCapture(); //当你不在需要继续获得鼠标消息就要应该调用ReleaseCapture()释放掉
      isResizing.value = false;
      SheetInstance.spreadsheet.sheet.reload();
      SheetInstance.spreadsheet.sheet.toolbar.reRenderFunc();
      console.log(SheetInstance);

    }

    resize[0].setCapture && resize[0].setCapture(); //该函数在属于当前线程的指定窗口里设置鼠标捕获
    return false;
  }
}

onMounted(()=>{
  dragControllerDiv()
})

</script>

<style>
.box {
  width: 100%;
  height: 96vh;
  background-color: white;
  display: flex;
  position: fixed;
}

.resize {
  cursor: col-resize;
  background-color: #E3E3E3;
  width: 5px;
  height: 100%;
}

#workSpaceTransition {
  transition: width 0.4s ease; /* 调整过渡时间和缓动函数 */
}

</style>



