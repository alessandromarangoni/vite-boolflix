<script >
import HelloWorld from './components/HelloWorld.vue'
import headerApp from './components/headerApp.vue';
import { store } from './data/store'
export default {
  components: {
    store,
    HelloWorld,
    headerApp,
  }
}
</script>

<template>
  <headerApp />
  <HelloWorld />
</template>

<style scoped></style>
