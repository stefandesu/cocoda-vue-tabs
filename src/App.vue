<template>
  <div id="app">
    <div>
      <h1>cocoda-vue-tabs</h1>
      <a href="https://github.com/stefandesu/cocoda-vue-tabs">https://github.com/stefandesu/cocoda-vue-tabs</a>
      <h2>Examples:</h2>
      <h3>Simple tabs with no extras</h3>
      <example-01 />
      <h3>Dynamically add, change, or remove tabs</h3>
      <example-02 />
      <h3>Tabs with fill and variable height content</h3>
      <example-03 />
      <h3>Tabs with fixed width and height (demonstrates scrolling)</h3>
      <example-04 />
    </div>
  </div>
</template>

<script>
import Example01 from "./Example01"
import Example02 from "./Example02"
import Example03 from "./Example03"
import Example04 from "./Example04"

export default {
  name: "App",
  components: {
    Example01,
    Example02,
    Example03,
    Example04,
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  padding: 10px;
}
#app > div {
  max-width: 800px;
  margin: 60px auto 0 auto;
}
</style>
