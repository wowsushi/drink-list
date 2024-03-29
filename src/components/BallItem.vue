<script setup>
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
</script>

<template>
  <div class="ball">{{ number }}</div>
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
  animation: move 2s infinite;
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
