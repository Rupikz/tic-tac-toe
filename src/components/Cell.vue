<template>
  <td class="cell" @click="slap" >
    <span class="figure" :class="mark"></span>
  </td>
</template>

<script>
import emitter from '../eventHub';

export default {
  name: 'Cell',
  props: ['id'],
  data() {
    return {
      mark: '',
      exists: false,
    };
  },
  methods: {
    slap() {
      if (!this.exists) {
        this.mark = this.$parent.currentPlayer;
      }
      emitter.emit('slap', {
        id: this.id,
        exists: this.exists,
      });

      this.exists = true;
    },
  },
  created() {
    emitter.on('clear-cell', () => {
      this.mark = '';
      this.exists = false;
    });
  },
};
</script>

<style>
  td {
    border: 15px #2c3e50 solid;
    width: 80px;
    height: 80px;
    background-color: #34495e;
  }

  .figure {
    position: relative;
    top: 0;
    right: 0;
    width: 32px;
    height: 32px;
  }

  /* X */

  .cross:before, .cross:after {
    content: "";
    position: absolute;
    height: 33px;
    width: 5px;
    top: 2px;
    left: -2px;
    background-color: #f1c40f;
  }
  .cross:before {
    transform: rotate(45deg);
  }
  .cross:after {
    transform: rotate(-45deg);
  }

  /* O */

  .zero:before,
  .zero:after {
    content: "";
    position: absolute;
    top: 0;
    left: -21px;
    width: 32px;
    height: 32px;
    border: 5px solid #217ad3;
    -moz-border-radius: 50px 50px 50px 50px;
    border-radius: 50px 50px 50px 50px;
  }

</style>
