<script setup lang="ts">
import VueDrawer from './components/VueDrawer.vue'
import { Ref, ref } from 'vue'
const isOpened: Ref<boolean> = ref(false)

</script>

<template>
  <div>
    <button
      @click="isOpened = true"
    >Click to open the drawer</button>
  </div>
  <VueDrawer
      v-model="isOpened"
    position="right"
    background-color="#CCC"
  >
    Slot content goes here
  </VueDrawer>
</template>

<style scoped>

</style>
