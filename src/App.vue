<template>
  <div class="container">
    <h1>TIC TAC TOE</h1>
    <h4>MATCH №{{ match }}</h4>
    <Dashboard :wins="wins" />
    <Grid />
    <Button @click="restartGame"/>
  </div>
</template>

<script>
import Dashboard from './components/Dashboard.vue';
import Grid from './components/Grid.vue';
import Button from './components/Button.vue';

export default {
  name: 'App',
  components: {
    Dashboard,
    Grid,
    Button,
  },
  data() {
    return {
      match: 0,
      wins: {
        O: 0,
        X: 0,
      },
    };
  },
  methods: {
    restartGame() {
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
</style>
