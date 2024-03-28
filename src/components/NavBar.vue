<script setup>
import IconMenu from './icons/IconMenu.vue'
</script>

<template>
  <header>
    <nav class="nav">
      <IconMenu />
    </nav>
  </header>
</template>

<style scoped>
.nav {
  display: flex;
  background-color: white;
  height: 40px;
  justify-content: right;
  padding: 0.5rem;
}
</style>
