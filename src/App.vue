<style>
:root {
  --box-shadow: #000000;
  --box-border: #6f7579;
  --input-outline: #5b7277b9;
  --prime-dark-color: black;
  --prime-light-color: rgb(187, 187, 187);
}

* {
  padding: 0;
  margin: 0;
  color: var(--prime-dark-color);
  box-sizing: border-box;
  font-family: sans-serif;
}

body {
  font-size: 1.2rem;
}
</style>

<template>
  <div id="app">
    <AppLayout tableData="tableData" />
  </div>
</template>

<script>
import AppLayout from './components/AppLayout.vue'

export default {
  name: 'App',
  components: {
    AppLayout
  }
}
</script>