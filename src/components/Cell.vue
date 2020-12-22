<template>
  <td class="cell" @click="slap" >
    <span class="figure" :class="mark"></span>
  </td>
</template>

<script>
import emitter from '../assets/eventHub';

export default {
  name: 'Cell',
  props: ['id'],
  data() {
    return {
      mark: '',
      exists: false,
      freeze: false,
    };
  },
  methods: {
    slap() {
      if (!this.exists && !this.freeze) {
        this.mark = this.$parent.currentPlayer;
        this.exists = true;

        emitter.emit('slap', {
          id: this.id,
          exists: this.exists,
        });
      }
    },
  },
  created() {
    emitter.on('clear-cell', () => {
      this.mark = '';
      this.exists = false;
      this.freeze = false;
    });

    emitter.on('win', () => {
      this.freeze = true;
    });
  },
};
</script>

<style>
  .cell {
    border: 10px #2c3e50 solid;
    width: 80px;
    height: 80px;
    background-color: #34495e;
  }

  .cell:hover {
    background-color: #364758;
  }

  .figure {
    position: relative;
    top: 0;
    right: 0;
    width: 32px;
    height: 32px;
  }

  /* X */

  .figure.cross:before, .figure.cross:after {
    content: "";
    position: absolute;
    height: 45px;
    width: 5px;
    top: -5px;
    left: -3px;
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
    content: "";
    position: absolute;
    top: 0px;
    left: -21px;
    width: 32px;
    height: 32px;
    border: 5px solid #217ad3;
    -moz-border-radius: 50px 50px 50px 50px;
    border-radius: 50px 50px 50px 50px;
  }

</style>
