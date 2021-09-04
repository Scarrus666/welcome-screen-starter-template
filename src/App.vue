<template>
  <div id="app">
  {{ title }}
  <!-- html files go here -->
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
        title: "Welcome to Opportunity"
      };
    }
}
</script>

<style>
/* css styles go here */

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
