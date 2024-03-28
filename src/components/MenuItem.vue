<script setup>
defineProps({
  menuData: {
    type: Array
  }
})
import { ref } from 'vue'

const activeMenu = ref('')
const isActive = (key) => {
  return activeMenu.value === key
}
const handleClickMenuItem = (key) => {
  activeMenu.value = isActive(key) ? '' : key
}
</script>
<template>
  <template v-for="item in menuData" :key="item.key">
    <li :class="['menu-item-wrapper', { active: isActive(item.key) }]">
      <h3
        :class="['menu-item', { active: isActive(item.key) }]"
        @click="handleClickMenuItem(item.key)"
      >
        {{ item.text }}
      </h3>
      <ul class="menu-sub-item-container" v-if="item.children && isActive(item.key)">
        <MenuItem :menuData="item.children" />
      </ul>
    </li>
  </template>
</template>

<style scoped>
.menu-item-wrapper.active {
  background-color: var(--bg-menu-item-active);
}

.menu-item {
  margin: 0;
  padding: 1rem;
  color: white;
}

.menu-item.active {
  color: yellow;
}

.menu-sub-item-container {
  padding-left: 1rem;
}
</style>
