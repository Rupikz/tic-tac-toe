<template>
  <div class="grid">
    <table>
      <tr>
        <Cell name="1" @slap="slapBroker" />
        <Cell name="2" @slap="slapBroker"/>
        <Cell name="3" @slap="slapBroker"/>
      </tr>
      <tr>
        <Cell name="4" @slap="slapBroker"/>
        <Cell name="5" @slap="slapBroker"/>
        <Cell name="6" @slap="slapBroker"/>
      </tr>
      <tr>
        <Cell name="7" @slap="slapBroker"/>
        <Cell name="8" @slap="slapBroker"/>
        <Cell name="9" @slap="slapBroker"/>
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
  methods: {
    slapBroker(id) {
      this.$emit('slap', id);
    },
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
