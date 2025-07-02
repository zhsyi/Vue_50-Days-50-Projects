
<template>
  <div class="container">
  <section class="bg" :style="{filter:`blur(${blurAmount})`}"> </section> 
  <!--``格式是用来说明这是一个ES6 语法，也就是模板字符串，在模板字符串内可以用普通文本格式打字。-->
  <!--  反引号绑定滤镜，$用来插入变量   -->
  <!-- px用来表示blur的单位-->
  <!--section 为背景设置-->

    <div class="loading-text" :style="{opacity: textOpacity}">{{ load }}%</div>
    <!--百分号显示-->
  </div>
</template>

<script setup>
import {ref, computed, onMounted, onBeforeUnmount} from 'vue'

const load = ref(0)
const interval = ref(null)
const scale = (num, in_min, in_max, out_min, out_max) => {
// 这个的bur
  return((num - in_min) * (out_max - out_min))/(in_max - in_min) + out_min
}
const blurAmount = computed(() => `${scale (load.value, 0, 100, 30, 0)}px`)
const textOpacity = computed(() => `${scale(load.value, 0, 100, 1,0)}px`)

const blurring = () => {
  load.value++
  if(load.value> 99){
    clearInterval(interval.value)
  }
}

onMounted(() => {
  interval.value = setInterval(blurring,  30)
})

onBeforeUnmount(() => {
  clearInterval(interval.value)
})
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Ubuntu');

*{
  box-sizing: border-box;
}

.container{
font-family:'ubuntu', sans-serif;
display: flex;
align-items: center;
justify-content: center;
height: 100vh;
overflow: hidden;
margin: 0;
position: relative;

}

.bg{
  background:url('https://images.unsplash.com/photo-1576161787924-01bb08dad4a4?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2104&q=80')
    no-repeat center center/cover;
  position: absolute;
  top:-30px;
  left:-30px;
  width: calc(100vw + 60px);
  height: calc(100vh + 60px);
  z-index:-1;
  filter: blur(0px);

}
.loading-text{
  font-size: 50px;
  color:#fff
}




</style>