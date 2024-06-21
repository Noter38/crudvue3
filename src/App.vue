<!-- src/components/FormComponent.vue -->
<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>Aplicación CRUD con Vue.js</h1>
    <CrudComponent />
  </div>
</template>

<script>
import CrudComponent from './components/CrudComponent.vue';

export default {
  components: {
    CrudComponent,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin-top: 60px;
}
</style>
