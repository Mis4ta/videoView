<script setup>
// 导入刚才下载的西瓜视频
import { onMounted, ref } from "@vue/runtime-core";
import Player from "xgplayer";
import { useIntersectionObserver } from "@vueuse/core";
const disabled = ref(true);
onMounted(() => {
  let player = new Player({
    id: "mse",
    url: require("./assets/video/我是真ikun.mp4"),
    width: "100%",
    height: "100%",
  });
  const { stop } = useIntersectionObserver(
    document.getElementById("videoContainer"),
    ([{ isIntersecting }]) => {
      // console.log(isIntersecting);
      disabled.value = isIntersecting;
    }
  );
});
</script>
<template>
  <!-- 要传送到的小视频播放窗口 -->
  <div id="small"></div>
  <!-- 被监听出入视口的展位元素 -->
  <div class="observeContainer" id="videoContainer"></div>
  <!-- 初始播放的大视频窗口 -->
  <div class="bigBox">
    <teleport to="#small" :disabled="disabled">
      <div id="mse"></div>
    </teleport>
  </div>
  <!-- 模拟滚动 -->
  <div style="height: 2000px"></div>
</template>

<style lang="less">
#small {
  position: fixed;
  bottom: 20px;
  right: 20px;
  width: 200px;
  height: 140px;
}
.observeContainer {
  width: 600px;
  height: 420px;
  position: absolute;
}
.bigBox {
  width: 600px;
  height: 420px;
}
</style>
