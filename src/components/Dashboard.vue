<template>
  <div class="dashboard">
    <div class="score score-left">{{ wins.X }}</div>
    <span class="separator"></span>
    <div class="score score-right">{{ wins.O }}</div>
  </div>
</template>

<script>
export default {
  props: {
    wins: Object,
  },
  name: 'Dashboard',
};
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
    width: 8px;
    background-color: #e74c3c;
  }

  .score {
    padding: 15px 0;
    background-color: #f1c40f;
    width: 100%;
    vertical-align: bottom;
  }

  .score-left {
    border-radius: 15px 0 0 0;
  }

  .score-right {
    border-radius: 0 15px 0 0;
  }
</style>
