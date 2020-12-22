<template>
  <div class="grid">
    <table>
      <tr>
        <Cell id="1" />
        <Cell id="2" />
        <Cell id="3" />
      </tr>
      <tr>
        <Cell id="4" />
        <Cell id="5" />
        <Cell id="6" />
      </tr>
      <tr>
        <Cell id="7" />
        <Cell id="8" />
        <Cell id="9" />
      </tr>
    </table>
  </div>
</template>

<script>
import player from '../assets/playersType';
import emitter from '../eventHub';
import Cell from './Cell.vue';

export default {
  components: {
    Cell,
  },
  name: 'Grid',
  data() {
    return {
      currentPlayer: player.zero,
      position: {
        [player.zero]: [],
        [player.cross]: [],
      },
      winConditions: [
        [1, 2, 3], [4, 5, 6], [7, 8, 9], // rows
        [1, 4, 7], [2, 5, 8], [3, 6, 9], // columns
        [1, 5, 9], [3, 5, 7], // diagonals
      ],
    };
  },
  methods: {

  },
  created() {
    emitter.on('slap', (event) => {
      if (!event.exists) {
        this.currentPlayer = this.currentPlayer === player.zero ? player.cross : player.zero;
      }
    });
  },
};
</script>

<style>
  .grid {
    width: 100%;
    border-radius: 15px 15px 0 0;
    border: 0;
    color: #2c3e50;
  }

  table {
    width: 100%;
    table-layout: fixed;
    border-collapse: collapse;
  }
</style>
