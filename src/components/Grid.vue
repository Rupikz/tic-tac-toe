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
import _ from 'lodash'
import player from '../assets/playersType'
import emitter from '../assets/eventHub'
import Cell from './Cell.vue'

export default {
  name: 'Grid',
  components: {
    Cell
  },
  data() {
    return {
      currentPlayer: player.zero,
      position: {
        [player.zero]: [],
        [player.cross]: []
      },
      winConditions: [
        [1, 2, 3],
        [4, 5, 6],
        [7, 8, 9],
        [1, 4, 7],
        [2, 5, 8],
        [3, 6, 9],
        [1, 5, 9],
        [3, 5, 7]
      ]
    }
  },
  created() {
    emitter.on('slap', (msg) => {
      this.addStep(+msg.id)
        .checkWinner()
        .changePlayer()
    })

    emitter.on('clear-grid', () => {
      emitter.emit('clear-cell')
      this.position[player.zero] = []
      this.position[player.cross] = []
    })
  },
  methods: {
    addStep(id) {
      this.position[this.currentPlayer].push(id)
      return this
    },

    changePlayer() {
      emitter.emit('current-player', this.currentPlayer)
      this.currentPlayer =
        this.currentPlayer === player.zero ? player.cross : player.zero
    },

    checkWinner() {
      const currentStateGrid = this.position[this.currentPlayer].sort()
      if (currentStateGrid.length >= 3) {
        this.winConditions.forEach((con) => {
          const intersection = _.intersection(con, currentStateGrid)
          if (JSON.stringify(intersection) === JSON.stringify(con)) {
            emitter.emit('win', this.currentPlayer)
          }
        })
      }
      return this
    }
  }
}
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
