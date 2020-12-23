<template>
  <td class="cell" @click="slap">
    <span class="figure" :class="mark"></span>
  </td>
</template>

<script>
import emitter from '../assets/eventHub'

export default {
  name: 'Cell',
  props: {
    id: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      mark: '',
      exists: false,
      freeze: false
    }
  },
  created() {
    emitter.on('clear-cell', () => {
      this.mark = ''
      this.exists = false
      this.freeze = false
    })

    emitter.on('win', () => {
      this.freeze = true
    })
  },
  methods: {
    slap() {
      if (!this.exists && !this.freeze) {
        this.mark = this.$parent.currentPlayer
        this.exists = true

        emitter.emit('slap', {
          id: this.id,
          exists: this.exists
        })
      }
    }
  }
}
</script>

<style>
.cell {
  position: relative;
  background-clip: padding-box;
  border: 10px #2c3e50 solid;
  width: 80px;
  height: 86px;
  background-color: #34495e;
}

.cell:hover {
  background-color: #364758;
}

.figure {
  width: 32px;
  height: 32px;
}

button,
button:active,
button:focus {
  outline: none;
}

/* X */

.figure.cross:before,
.figure.cross:after {
  content: '';
  position: absolute;
  height: 45px;
  width: 5px;
  right: 41px;
  top: 22px;
  background-color: #f1c40f;
}
.figure.cross:before {
  transform: rotate(45deg);
}
.figure.cross:after {
  transform: rotate(-45deg);
}

/* O */

.figure.zero:before,
.figure.zero:after {
  content: '';
  position: absolute;
  width: 32px;
  height: 32px;
  right: 22px;
  top: 25px;
  border: 5px solid #217ad3;
  -moz-border-radius: 50px 50px 50px 50px;
  border-radius: 50px 50px 50px 50px;
}
</style>
