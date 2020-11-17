<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: "app",
};
</script>

<style lang="scss">

* {
  margin: 0;
  padding: 0;
  list-style-type: none;
}

:root {
  font-size: 10px;
}

body {
  background: #607D8B;
}
#app {
  margin-top: 3rem;
}
</style>
