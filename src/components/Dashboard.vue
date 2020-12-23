<template>
  <div class="dashboard">
    <div
      class="score score-left"
      :class="{ 'dashboard-zero': player === 'cross' }"
    >
      {{ wins.zero }}
    </div>
    <span class="separator"></span>
    <div
      class="score score-right"
      :class="{ 'dashboard-cross': player === 'zero' }"
    >
      {{ wins.cross }}
    </div>
  </div>
</template>

<script>
import player from '../assets/playersType'
import emitter from '../assets/eventHub'

export default {
  name: 'Dashboard',
  props: {
    wins: player
  },
  data() {
    return {
      player: 'cross'
    }
  },
  created() {
    emitter.on('current-player', (name) => {
      this.player = name
    })
  }
}
</script>

<style>
.dashboard {
  display: flex;
  flex-direction: row;
  justify-content: center;
  font-size: 1.4em;
  color: #ffffff;
}

.separator {
  position: relative;
  content: '';
  width: 13px;
  background-color: #2c3e50;
}

.score {
  padding: 15px 0;
  width: 100%;
  vertical-align: bottom;
}

.score-left {
  border-radius: 15px 0 0 0;
  background-color: #217ad3;
}

.score-right {
  border-radius: 0 15px 0 0;
  background-color: #f1c40f;
}

.dashboard-zero {
  box-shadow: -5px -5px 20px #217ad3;
  z-index: -1;
}

.dashboard-cross {
  box-shadow: 5px -5px 20px #f1c40f;
  z-index: -1;
}
</style>
