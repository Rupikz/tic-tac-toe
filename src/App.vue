<template>
  <div class="container">
    <h1>TIC TAC TOE</h1>
    <h4 v-if="gameOver" class="winner" :class="gameOver">{{ gameOver }} Won!</h4>
    <h4 v-else>MATCH №{{ match }}</h4>
    <Dashboard :wins="wins" />
    <Grid />
    <button class="restart" @click="restartGame">Restart</button>
  </div>
</template>

<script>
import Dashboard from './components/Dashboard.vue';
import Grid from './components/Grid.vue';
import emitter from './assets/eventHub';
import player from './assets/playersType';

export default {
  name: 'App',
  components: {
    Dashboard,
    Grid,
  },
  data() {
    return {
      match: 1,
      gameOver: '',
      wins: {
        [player.zero]: 0,
        [player.cross]: 0,
      },
    };
  },
  methods: {
    restartGame() {
      emitter.emit('clear-grid');
      this.match += 1;
      this.gameOver = false;
    },
  },
  created() {
    emitter.on('win', (winer) => {
      this.wins[winer] += 1;
      this.gameOver = winer;
    });
  },

};
</script>

<style>
body {
  font-family: 'Oswald', sans-serif;
  font-weight: 700;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px 0;
  font-style: normal;
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
  cursor: pointer;
}

.restart:hover {
  background-color: #c95143;
  color: #ffffff
}

.winner {
  font-weight: 700;
}

.winner:first-letter {
  text-transform: uppercase;
}

.winner.zero {
  color: #217ad3;
}

.winner.cross {
  color: #f1c40f;
}
</style>
