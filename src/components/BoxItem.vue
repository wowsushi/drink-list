<script setup>
defineProps({
  isFlicking: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <div :class="['box', { isFlicking }]"></div>
</template>

<style scoped>
.box {
  height: 100px;
  border: black solid 2px;
  background: radial-gradient(circle, rgba(113, 81, 95, 1) 81%, rgba(0, 0, 0, 1) 100%);
}

.box.isFlicking {
  animation: flicking 0.4s ease;
  animation-iteration-count: infinite;
}

@keyframes flicking {
  from {
    opacity: 100%;
  }

  to {
    opacity: 60%;
  }
}
</style>
