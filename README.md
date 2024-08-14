# Vue drawer

Simple Drawer component written in vue 3 composition API and typescript.
It has he following behavior:
* The content is displayed once the drawer animation is finished.
* The content is hidden before the drawer animation is started.


# Usage 

## Install it

```
#If using yarn
yarn add vue3-drawer

#If using npm
npm i vue3-drawer

#If using pnpm
pnpm add vue3-drawer
```

## In your entrypoint, import the CSS

```
//main.ts

import 'vue3-drawer/style.css'

```

## Then import and use the component as you wish

```
<script setup lang="ts">
import { VueDrawer } from 'vue3-drawer'
...

//declare model
const isDrawerOpen: Ref<boolean> = ref(false)

</script>

<template>
  ...
  
  <VueDrawer
    v-model="isDrawerOpen"
    position="right"
    background-color="#CCC"
  >
    Slot content goes here
  </VueDrawer>
</template>
```


# Contributing

Run dev server:
```
 pnpm run dev
```

Build using:

```
 pnpm run build
```

