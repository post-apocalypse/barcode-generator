<template>
<NavMenuIcon @click="isActive = !isActive" :class="{ 'active': isActive }" />
<Transition name="main">
  <div v-show="isActive" class="menu-wrapper">
    <div class="menu">
      <slot name="theme"></slot>
      <div class="_row">
        <slot name="translation"></slot>
        <div class="_br"></div>
        <slot name="contacts"></slot>
      </div>
    </div>
  </div>
</Transition>
</template>

<script setup>
import { ref } from 'vue'
import NavMenuIcon from './NavMenuIcon.vue'
import { useEventListener } from '@vueuse/core'

const isActive = ref(false)
useEventListener(document, 'click', (evt) => {
  if (!evt.target.closest(['.menu-icon', '.menu-wrapper'])) {
    isActive.value = false
}
})
</script>

<style scoped lang="scss">
.menu-wrapper {
  background-color: var(--bg-c);
  position: fixed;
  top: 73px;
  right: 15px;
  width: 200px;
  height: 100px;
  z-index: 40;
  padding: var(--space);
  border-radius: var(--br-rad);
}

.menu {
  display: flex;
  width: 100%;
  height: 100%;
  flex-direction: column;
  gap: var(--space);
  justify-content: center;
}
</style>
