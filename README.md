# Vue drawer

Simple Drawer component written in vue 3 composition API and typescript.
It has he following behavior:
* The content is displayed once the drawer animation is finished.
* The content is hidden before the drawer animation is started.


# Usage 

```
  <VueDrawer
    v-model="isOpened"
    position="right"
    background-color="#CCC"
  >
    Slot content goes here
  </VueDrawer>
```


# Development

Run 
```
 pnpm run dev
```

# Build

Run
```
 pnpm run build
```


# Thanks

* https://blog.ayitinya.me/articles/how-to-create-and-publish-vue-component-to-npm
for providing step by step howto to publish package to npm

