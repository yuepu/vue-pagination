<template>
  <div id="app">
    <Pagination></Pagination>
  </div>
</template>
<script>
import Pagination from './components/Pagination/Pagination.vue';

export default {
  name: 'app',
  components: {
    Pagination
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
