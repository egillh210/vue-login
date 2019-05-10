<template>
  <div id="app">
    <div class="wrapper">
      <Login />
    </div>
  </div>
</template>

<script>
import Login from './components/Login';

export default {
  name: 'app',
  components: {
    Login,
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
.wrapper {
  display: inline-block;
  margin-top: 150px;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  font-weight: 100;
  color: #000000;
  height: 100vh;
  width: 100vw;
  background-color: #f4f4f4;
}
</style>
