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
    ballRef.value.style.left = x + 'px'
    ballRef.value.style.top = y + 'px'
    requestAnimationFrame(draw)
  }

  ballRef.value.style.position = 'fixed'
  ballRef.value.style.left = startX + 'px'
  ballRef.value.style.top = startY + 'px'
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

  move({
    startX: ballPosition.x,
    startY: ballPosition.y,
    endX: props.to[0],
    endY: props.to[1]
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
  position: absolute;
  /* animation: move 2s infinite; */
}

.ball:first-child,
.ball:nth-child(2) {
  top: 35px;
}

.ball:nth-child(3),
.ball:nth-child(4) {
  top: 245px;
}

.ball:first-child,
.ball:nth-child(3) {
  left: 45px;
}

.ball:nth-child(2),
.ball:nth-child(4) {
  left: 305px;
}

@keyframes move {
  from {
    transform: translateX(0);
  }

  to {
    transform: translateX(300px);
  }
}
</style>
