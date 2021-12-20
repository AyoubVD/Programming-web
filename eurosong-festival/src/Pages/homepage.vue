<template>
  <div id="app">
    <div v-if="page == 'home'">
      <h1>
        Eurosong voting app
      </h1>

      <button @click="redirect('game')">
        Show game
      </button>

      <button @click="redirect('ranking')">
        Show ranking
      </button>
    </div>

    <div v-if="page == 'ranking'">
      <button @click="redirect('home')">
        Go back home
      </button>
      <h1>
        Game
      </h1>
    </div>

    <div v-if="page == 'game'">
      <button @click="redirect('home')">
        Go back home
      </button>
      <h1>
        Ranking
      </h1>
    </div>

  </div>
</template>

<script> 
  import HelloWorld from './components/HelloWorld.vue';
  export default { 
    name: 'App', 
    components: {
    }, 
    data() { 
      return {
        page: "home"
      } 
    },
    methods: {
      redirect(page) {
        this.page = page;
      }
    }
  } 
</script>

<style lang="scss"> 
  @import "./scss/style.scss"; 
</style>