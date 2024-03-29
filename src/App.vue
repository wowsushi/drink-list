<script setup>
import NavBar from './components/NavBar.vue'
import BoxItem from './components/BoxItem.vue'
import BallItem from './components/BallItem.vue'
</script>

<template>
  <NavBar />
  <main class="main-wrapper">
    <div class="box-wrapper">
      <template v-for="index in 9" :key="index">
        <BoxItem :isFlicking="[3, 5, 9].includes(index)" />
      </template>
      <div class="ball-wrapper">
        <template v-for="index in 100" :key="index">
          <BallItem :to="[180, 422]" :number="0" />
        </template>
      </div>
    </div>
  </main>
</template>

<style scoped>
.main-wrapper {
  height: calc(100vh - var(--height-menu-bar));
  display: flex;
  align-items: center;
}
.box-wrapper {
  position: relative;
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  gap: 0.25rem;
  margin: 0.25rem;
  overflow: hidden;
}

.ball-wrapper {
  position: absolute;
  inset: 0;
}
</style>
