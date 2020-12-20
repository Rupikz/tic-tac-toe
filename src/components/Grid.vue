<template>
  <div class="grid">
    <table>
      <tr>
        <Cell name="1" />
        <Cell name="2" />
        <Cell name="3" />
      </tr>
      <tr>
        <Cell name="4" />
        <Cell name="5" />
        <Cell name="6" />
      </tr>
      <tr>
        <Cell name="7" />
        <Cell name="8" />
        <Cell name="9" />
      </tr>
    </table>
  </div>
</template>

<script>
import Cell from './Cell.vue';

export default {
  components: {
    Cell,
  },
  name: 'Grid',
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
