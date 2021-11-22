<template>
  <div id="app">
    <nav class="c-nav">
      <ul class="c-nav-list">
        <li class="c-nav-list-item">Home</li>
        <li class="c-nav-list-item">Contact</li>
      </ul>
    </nav>
    <img alt="Vue logo" src="./assets/logo.png">
    <h1>Hello not online yet</h1>
    <h2>NVM, it's online</h2>
  </div>
</template>

<script>
import style from './scss/style.scss'

export default {
  name: 'App'
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
