## teleport(传送门)

​		需求分析:

​		1:初始化一个视频播放

​		2.大视频播放区域如果在视口外,小窗口出现

​		3.大视频和小视频切换时候保持视频状态不变

​		

​		思路分析:

​		1.video/成熟的视频插件

​		2.监控大视频是否在视口区域   vueUse三方插件(会给一些封装好的api)

​		3.内置组件Teleport 保持dom状态的前提下完成

















### 基本h-c

<template>
  <!-- 要传送到的小视频播放窗口 -->
  <div id="small"></div>
  <!-- 被监听出入视口的展位元素 -->
  <div class="observeContainer" id="videoContainer"></div>
  <!-- 初始播放的大视频窗口 -->
  <div class="bigBox">
      <div id="mse"></div>
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
  border: 1px solid;
}
.observeContainer {
  width: 600px;
  height: 420px;
  position: absolute;
}
.bigBox {
  width: 600px;
  height: 420px;
  border: 1px solid;
}
</style>




### 使用的播放器插件:西瓜播放器

[西瓜播放器 | 快速上手 (bytedance.com)](https://v2.h5player.bytedance.com/gettingStarted/#安装)



导入刚下载的西瓜视频

import Player from "xgplayer";





实例化

```js
let player = new Player({
  id: 'mse',
  url: '//abc.com/**/*.mp4'
});
```



在挂载的时候

onMouted(()=>{

​	引入实例化对象

})





### 使用vueUse第三方插件

[VueUse | VueUse](https://vueuse.org/)

搜索 observe  点击 useIntersectionObserver



在 Usage 里面 复制

```js
  const { stop } = useIntersectionObserver(      target,      ([{ isIntersecting }], observerElement) => {        targetIsVisible.value = isIntersecting      },    )
```

当然我们并不能直接使用第三方插件 下载并引入

```
import { useIntersectionObserver } from '@vueuse/core'
```





### 引出Teleport（传送门）

[Vue.js - 渐进式 JavaScript 框架 | Vue.js (vuejs.org)](https://cn.vuejs.org/)

点击深度指南中的内置组件