<script setup>
import { ref, onMounted } from 'vue'
const props = defineProps({
  number: {
    type: Number
  },
  to: {
    type: Array
  }
})

const move = ({ startX, startY, endX, endY }) => {
  let duration = 2000
  let startTimeStamp = null

  const inOutQuad = (n) => {
    n *= 2
    if (n < 1) return 0.5 * n * n
    return -0.5 * (--n * (n - 2) - 1)
  }

  const draw = (nowTimeStamp) => {
    if (nowTimeStamp - startTimeStamp >= duration) startTimeStamp = nowTimeStamp
    const percentage = (nowTimeStamp - startTimeStamp) / duration
    const value = inOutQuad(percentage)
    const x = startX + (endX - startX) * value
    const y = startY + (endY - startY) * value
    ballRef.value.style.transform = `translate(${x}px, ${y}px)`
    requestAnimationFrame(draw)
  }

  ballRef.value.style.transform = `translate(${startX}px, ${startY}px)`
  requestAnimationFrame(draw)
}

const ballRef = ref(null)
onMounted(() => {
  const ballPosition = (() => {
    const rect = ballRef.value.getBoundingClientRect()
    return {
      x: rect.x,
      y: rect.y
    }
  })()
  const startPosition = (() => {
    const x = Math.random() * (window.innerWidth - 0) + 0
    const y = Math.random() * (window.innerHeight - 0) + 0
    return {
      x,
      y
    }
  })()
  move({
    startX: startPosition.x - ballPosition.x,
    startY: startPosition.y - ballPosition.y,
    endX: props.to[0] - ballPosition.x,
    endY: props.to[1] - ballPosition.y
  })
})
</script>

<template>
  <div ref="ballRef" class="ball">{{ number }}</div>
</template>

<style scoped>
.ball {
  width: 30px;
  height: 30px;
  background-color: var(--bg-ball);
  border-radius: 100%;
  line-height: 30px;
  text-align: center;
  position: fixed;
  will-change: transform;
}
</style>
