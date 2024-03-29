<script setup>
import { ref, onMounted } from 'vue'
defineProps({
  number: {
    type: Number
  },
  from: {
    type: String
  },
  to: {
    type: String
  }
})

const move = () => {
  let startx = 0
  let endx = 300
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
    const x = startx + (endx - startx) * value
    ballRef.value.style.transform = `translateX(${x}px)`
    requestAnimationFrame(draw)
  }

  requestAnimationFrame(draw)
}
const ballRef = ref(null)
onMounted(() => {
  move()
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
