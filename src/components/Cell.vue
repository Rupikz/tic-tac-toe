<template>
  <td class="cell" @click="slap" >
    <span class="figure" :class="mark"></span>
  </td>
</template>

<script>
import emitter from '../eventHub';

export default {
  name: 'Cell',
  data() {
    return {
      mark: '', // cross or zero
      exists: false,
    };
  },
  methods: {
    slap() {
      console.log('lox');
      if (Math.random() > 0.5 && !this.exists) {
        this.mark = 'cross';
      } else {
        this.mark = 'zero';
      }
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
    background-color: #2c3e50;
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
    border: 5px solid #2c3e50;
    -moz-border-radius: 50px 50px 50px 50px;
    border-radius: 50px 50px 50px 50px;
  }

</style>
