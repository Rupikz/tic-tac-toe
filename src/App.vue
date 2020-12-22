<template>
  <div class="container">
    <h1>TIC TAC TOE</h1>
    <h4>MATCH №{{ match }}</h4>
    <Dashboard :wins="wins" />
    <Grid />
    <button class="restart" @click="restartGame">Restart</button>
  </div>
</template>

<script>
import Dashboard from './components/Dashboard.vue';
import Grid from './components/Grid.vue';
import emitter from './eventHub';
import player from './assets/playersType';

export default {
  name: 'App',
  components: {
    Dashboard,
    Grid,
  },
  data() {
    return {
      match: 0,
      wins: {
        [player.zero]: 0,
        [player.cross]: 0,
      },
    };
  },
  methods: {
    restartGame() {
      emitter.emit('clear-cell');
      this.match += 1;
    },
  },
};
</script>

<style>
#app {
  font-family: 'Oswald', sans-serif;
  font-weight: 700;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.container {
  width: 306px;
  margin: 0 auto;
}

.restart {
  width: 100%;
  background-color: #e74c3c;
  border-radius: 0 0 15px 15px ;
  font-size: 1.4em;
  padding: 15px 0;
  border: 0;
  color: #e0e0e0;
  transition: .3s ;
  text-transform: uppercase;
}

.restart:hover {
  background-color: #c95143;
  color: #ffffff
}
</style>
