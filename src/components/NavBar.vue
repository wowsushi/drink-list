<script setup>
import IconMenu from './icons/IconMenu.vue'
import MenuItem from './MenuItem.vue'
import { ref } from 'vue'
import menuData from '../menuData.json'

const isSideBarOpen = ref(false)
const handleToggleMenu = () => {
  isSideBarOpen.value = !isSideBarOpen.value
}
</script>

<template>
  <header>
    <nav class="nav">
      <IconMenu @click="handleToggleMenu" />
      <Teleport to="body">
        <aside
          :class="['aside-menu-wrapper', { show: isSideBarOpen }]"
          @click.self="handleToggleMenu"
        >
          <ul :class="['aside-menu', { show: isSideBarOpen }]">
            <MenuItem :menuData="menuData.data" />
          </ul>
        </aside>
      </Teleport>
    </nav>
  </header>
</template>

<style scoped>
.nav {
  display: flex;
  background-color: white;
  height: var(--height-menu-bar);
  justify-content: right;
  padding: 0.25rem;
}

.aside-menu-wrapper {
  position: fixed;
  inset: 0;
  pointer-events: none;
}

.aside-menu-wrapper.show {
  pointer-events: initial;
}

.aside-menu {
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  width: 250px;
  background-color: var(--bg-side-bar);
  transform: translateX(100%);
  transition: 0.3s ease-in-out;
  padding-left: 1rem;
}

.aside-menu.show {
  transform: translateX(0%);
}
</style>
