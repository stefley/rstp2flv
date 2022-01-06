<script setup>
import { onMounted, ref, onBeforeUnmount } from 'vue'
import flvjs from 'flv.js'

const player = ref(null)
const video = ref(null)
const init = () => {
  // 如果浏览器支持flvjs，则执行相应的程序
  if (flvjs.isSupported) {
    // 准备监控设备流地址
    const url = 'rtmp://videos3.e6yun.com:1935/live/11234400507-1-ems-16b9ad01-1777-4462-b5f0-052be01884c4'
    // 创建一个flvjs实例
    // 下面的ws://localhost:8888换成你搭建的websocket服务地址，后面加上设备流地址
    video.value = flvjs.createPlayer({
      type: "flv",
      isLive: true,
      url: "ws://localhost:8888/" + url
    })

    video.value.on("error",(err) => {console.log(err)})
  } 

   // 将实例挂载到video元素上面
   video.value.attachMediaElement(player.value)

   try {
     // 开始运行加载 只要流地址正常 就可以在h5页面中播放出画面了
     video.value.load()
     video.value.play()
   } catch (error) {
      console.log(error) 
   }
}
const destory = () => {
  // 页面销毁前 关闭flvjs
  video.value.destory()
}
onMounted(init)
onBeforeUnmount(destory)
defineProps({

})

</script>

<template>
  <div class="video-wrap">
    <video id="video-el" class="video" muted autoplay controls ref="player"></video>
  </div>
</template>
<style scoped>
  .video-wrap {
    width: 800px;
    height: 800px;
    margin: 100px auto;
  }
</style>
