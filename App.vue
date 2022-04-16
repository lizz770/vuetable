<template>
  <div id="app">
      <Components__table />
  </div>
</template>

<script>
import Components__table from './components/Components__table.vue'
export default {
  name:"App",
  components: {
    Components__table,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
