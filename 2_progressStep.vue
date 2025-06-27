<template>
  <div class="body">
    <div class="container">
      <div class="progress-container">
        <div class="progress" :style="{width: progressWidth}" ></div>
        <div :class="['circle', { active: currentActive >= 1 }]">1</div>
        <div :class="['circle', { active: currentActive >= 2 }]">2</div>
        <div :class="['circle', { active: currentActive >= 3 }]">3</div>
        <div :class="['circle', { active: currentActive >= 4 }]">4</div>
      </div>
      <div class="buttons">

      <button class="btn" @click="prev" :disabled="currentActive === 1">Prev</button>
      <button class="btn" @click="next" :disabled="currentActive === 4">Next</button>
      </div>
    </div>
  </div>
   
</template>

<script setup>
import {ref, computed} from 'vue' 

const currentActive = ref(1)

const progressWidth = computed(() => {
  // 计算进度条宽度（从 0% 到 100%）
  return `${((currentActive.value - 1) / 3) * 100}%`;
});

function prev (){
 if (currentActive.value > 1){currentActive.value --}

}

function next(){
    if (currentActive.value <4 ) {currentActive.value ++}
}





</script>

<style>
/* 原CSS内容直接粘贴至此 */@import url('https://fonts.googleapis.com/css?family=Muli&display=swap');

:root {
  --line-border-fill: #3498db;
  --line-border-empty: #e2e2e2;

}

* {
  box-sizing: border-box;
}

.body {
  background-color: #f1f1f1;
  font-family: 'Muli', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  overflow: hidden;
  margin: 0;
}

.container {
  text-align: center;
}

.progress-container {
  display: flex;
  justify-content: space-between;
  position: relative;
  margin-bottom: 30px;
  max-width: 100%;
  width: 350px;
}

.progress-container::before {
  content: '';
  background-color: var(--line-border-empty);
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  height: 4px;
  width: 100%;
  z-index: 1;
}

.progress {
  background-color: var(--line-border-fill);
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  height: 4px;
  width: 0%;
  z-index: 2;
  transition: 0.4s ease;
}

.circle {
  background-color: #f1f1f1;
  color:#e2e2e2;
  border-radius: 50%;
  height: 30px;
  width: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 3px solid var(--line-border-empty);
  transition: 0.4s ease;
  z-index: 3;
  position:relative;
}

.circle.active {
  border-color: var(--line-border-fill);
}

.btn {
  background-color: var(--line-border-fill);
  color: #fff;
  border: 0;
  border-radius: 6px;
  cursor: pointer;
  font-family: inherit;
  padding: 8px 30px;
  margin: 5px;
  font-size: 14px;
}

.btn:active {
  transform: scale(0.98);
}

.btn:focus {
  outline: 0;
}

.btn:disabled {
  background-color: var(--line-border-empty);
  cursor: not-allowed;
}
</style>