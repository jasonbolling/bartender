<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <br><br>
    <div>
      <input v-model="x" type="radio" value="view">
      <label for="viewOrders">View Orders</label>
      <input v-model="x" type="radio" value="place">
      <label for="placeOrder">Place an Order</label>
    </div>
    <ViewComponent v-if="x === 'view'"/>
    <AddComponent v-if="x === 'place'"/>
  </div>
</template>

<script>
import ViewComponent from './components/ViewComponent.vue'
import AddComponent from './components/AddComponent.vue'
export default {
  name: 'App',
  components: {
    ViewComponent,
    AddComponent,
  },
  data() {
    return{
      x: 'view',
    }
  },
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
