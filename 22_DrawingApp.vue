<template>
  <div class="drawing-app">
    <canvas ref="canvasRef" width="800" height="700"></canvas>
    <div class="toolbox">
      <button @click="decreaseSize">-</button>
      <span>{{ size }}</span>
      <button @click="increaseSize">+</button>
      <input type="color" v-model="color">
      <button @click="clearCanvas">X</button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const canvasRef = ref(null)
const ctx = ref(null)
const size = ref(10)
const color = ref('black')
const isPressed = ref(false)
let x = null
let y = null

onMounted(() => {
  ctx.value = canvasRef.value.getContext('2d')
  
  const canvas = canvasRef.value
  
  canvas.addEventListener('mousedown', handleMouseDown)
  document.addEventListener('mouseup', handleMouseUp)
  canvas.addEventListener('mousemove', handleMouseMove)
})

onBeforeUnmount(() => {
  const canvas = canvasRef.value
  
  canvas.removeEventListener('mousedown', handleMouseDown)
  document.removeEventListener('mouseup', handleMouseUp)
  canvas.removeEventListener('mousemove', handleMouseMove)
})

const handleMouseDown = (e) => {
  isPressed.value = true
  x = e.offsetX
  y = e.offsetY
}

const handleMouseUp = () => {
  isPressed.value = false
  x = null
  y = null
}

const handleMouseMove = (e) => {
  if (isPressed.value) {
    const x2 = e.offsetX
    const y2 = e.offsetY

    drawCircle(x2, y2)
    drawLine(x, y, x2, y2)

    x = x2
    y = y2
  }
}

const drawCircle = (x, y) => {
  ctx.value.beginPath()
  ctx.value.arc(x, y, size.value, 0, Math.PI * 2)
  ctx.value.fillStyle = color.value
  ctx.value.fill()
}

const drawLine = (x1, y1, x2, y2) => {
  ctx.value.beginPath()
  ctx.value.moveTo(x1, y1)
  ctx.value.lineTo(x2, y2)
  ctx.value.strokeStyle = color.value
  ctx.value.lineWidth = size.value * 2
  ctx.value.stroke()
}

const increaseSize = () => {
  size.value = Math.min(size.value + 5, 50)
}

const decreaseSize = () => {
  size.value = Math.max(size.value - 5, 5)
}

const clearCanvas = () => {
  ctx.value.clearRect(0, 0, canvasRef.value.width, canvasRef.value.height)
}
</script>

<style scoped>
.drawing-app {
  background-color: #f5f5f5;
  font-family: 'Roboto', sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  margin: 0;
}

canvas {
  border: 2px solid steelblue;
}

.toolbox {
  background-color: steelblue;
  border: 1px solid slateblue;
  display: flex;
  width: 804px;
  padding: 1rem;
}

.toolbox > * {
  background-color: #fff;
  border: none;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  font-size: 2rem;
  height: 50px;
  width: 50px;
  margin: 0.25rem;
  padding: 0.25rem;
  cursor: pointer;
}

.toolbox > *:last-child {
  margin-left: auto;
}
</style>  
