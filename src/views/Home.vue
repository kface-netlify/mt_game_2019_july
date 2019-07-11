<template>
  <div class="home">
    <Game msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Game from '@/components/Game.vue'

export default {
  name: 'home',
  components: {
    Game
  }
}
</script>
