<script setup lang="ts">

import { ref, computed, watch, defineModel } from 'vue'

type DrawerPosition = 'left' | 'right' | 'bottom'

interface Props {
  position?: DrawerPosition
  width?: string
  backgroundColor?: string
}

const props = withDefaults(defineProps<Props>(), {
  position: 'right',
  width: '300px',
  backgroundColor: 'white',
})

const isOpened = defineModel<boolean>()
const showContent = ref(false)

const drawerStyle = computed(() => {
  const style: Record<string, string> = {}
  if (props.position === 'bottom') {
    style.height = isOpened.value ? props.width : '0'
    style.width = '100%'
  } else {
    style.width = isOpened.value ? props.width : '0'
    style.height = '100%'
  }
  style.backgroundColor = props.backgroundColor
  return style
})

const onTransitionEnd = () => {
  if (isOpened.value) {
    showContent.value = true
  }
}
const onTransitionStart = () => {
  if (!isOpened.value) {
    showContent.value = false
  }
}

const closeDrawer = () => {
  isOpened.value = false
}

const positionClass = computed((): string => `vue-drawer--${props.position}`)

watch(() => isOpened, (newValue) => {
  if (!newValue) {
    showContent.value = false
  }
}, {immediate: true})

</script>

<template>
  <div
      class="vue-drawer"
  >
    <div
        v-if="isOpened"
        class="vue-drawer__overlay"
        @click="closeDrawer"
    ></div>

    <div
        :class="['vue-drawer__content', positionClass]"
        :style="drawerStyle"
        @transitionstart="onTransitionStart"
        @transitionend="onTransitionEnd"
    >
      <div v-if="showContent">
        <slot></slot>
      </div>
      <div
          v-if="$slots.close && isOpened"
          class="vue-drawer__close"
      >
        <slot name="close" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.vue-drawer__overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(211, 211, 211, 0.5);
  z-index: 998;
}

.vue-drawer__content {
  position: fixed;
  background-color: white;
  transition: all 0.3s ease-in-out;
  z-index: 999;
  overflow: hidden;
}

.vue-drawer__content > div {
  height: 100%;
}

.vue-drawer__close {
  position: absolute;
  top: 0;
  right: 0;
}

.vue-drawer--left {
  top: 0;
  left: 0;
  bottom: 0;
}

.vue-drawer--right {
  top: 0;
  right: 0;
  bottom: 0;
}

.vue-drawer--bottom {
  left: 0;
  right: 0;
  bottom: 0;
}
</style>
